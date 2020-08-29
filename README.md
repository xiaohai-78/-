# -
学生管理系统
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#pragma warning(disable:4996)

#define N 1024
#define MAXSIZE 32
#define WIDESIZE 65

typedef struct Student
{
	int code;
	char name[MAXSIZE];
	int age;
	char sex[MAXSIZE];
	int math;
	int chinese;
	int english;
	struct Student* next;
}Student;

Student* createList()
{
	Student* studentList = (Student*)malloc(sizeof(Student));
	return studentList;
}

Student* createNode()
{
	Student* newStu = (Student*)malloc(sizeof(Student));
	printf("学号:");
	scanf("%d", &newStu->code);
	printf("姓名:");
	scanf("%s", newStu->name);
	printf("年龄:");
	scanf("%d", &newStu->age);
	printf("性别:");
	scanf("%s", newStu->sex);
	printf("数学:");
	scanf("%d", &newStu->math);
	printf("语文:");
	scanf("%d", &newStu->chinese);
	printf("英语:");
	scanf("%d", &newStu->english);
	newStu->next = NULL;
	return newStu;
}

void fenge()
{
	printf("=====================================\n");
}


void showMsg(Student* stu)
{
	printf("%d\t%s\t%d\t%s\t%d\t%d\t%d\n", stu->code, stu->name,
		stu->age, stu->sex, stu->math, stu->chinese, stu->english);
}

Student* insertStudent(Student* head)
{
	int i, count;
	printf("请输入录入学生的人数");
	scanf("%d", &count);
	Student* tail = head;
	if (head)
	{
		for (i = 0;i < count;i++)
		{
			printf("=============输入第%d个学生的信息=============\n", i + 1);
			Student* newNode = createNode();
			tail->next = newNode;
			tail = tail->next;
		}
	}
	else {
		while (tail)
		{
			tail = tail->next;
		}
		for (i = 0;i < count;i++)
		{
			printf("=============请输入第%d个学生的信息=============\n", i + 1);
			Student* newNode = createNode();
			tail->next = newNode;
			tail = tail->next;
		}
	}

	printf("\t=========================\t\n");
	return head;
}

void deleteStudent(Student * studentList)
{
	printf("请输入学号:");
	int ditCode;
	scanf("%d", &ditCode);
	Student* preStudent = studentList;
	Student* afterStudent = studentList->next;
	if (afterStudent)
	{
		while(afterStudent	)
		{
			if (afterStudent->code == ditCode)
			{
				preStudent->next = afterStudent->next;
				free(afterStudent);
				break;
			}
			else
			{
				preStudent = afterStudent;
				afterStudent = afterStudent->next;
			}
		}
	}
	else
	{
		printf("没有这名学生的信息！");
	}
	printf("\t=========================\t\n");
	fenge();
}


void changeName(Student* stu)
{
	char newName[MAXSIZE];
	printf("请输入新的名字:");
	scanf("%s", newName);
	strcpy(stu->name, newName);
	showMsg(stu);
	printf("\t=========================\t\n");
	fenge();
}


void changeAge(Student* stu)
{
	int newAge;
	printf("请输入新的年龄:");
	scanf("%d", &newAge);
	stu->age = newAge;
	showMsg(stu);
	printf("\t=========================\t\n");
	fenge();
}


void changeMathScore(Student* stu)
{
	int newSocre;
	printf("请输入新的数学成绩:");
	scanf("%d", &newSocre);
	stu->math = newSocre;
	showMsg(stu);
	printf("\t=========================\t\n");
	fenge();

}


void changeChineseScore(Student* stu)
{
	int newSocre;
	printf("请输入新的语文成绩:");
	scanf("%d", &newSocre);
	stu->chinese = newSocre;
	showMsg(stu);
	printf("\t=========================\t\n");
	fenge();
}


void changeEnglishScore(Student* stu)
{
	int newSocre;
	printf("请输入新的英语成绩:");
	scanf("%d", &newSocre);
	stu->chinese = newSocre;
	showMsg(stu);
	printf("\t=========================\t\n");
	fenge();
}





void editStudent(Student* studentList)
{
	printf("请输入学号:");
	int ditCode;
	scanf("%d", &ditCode);
	Student* ditStu = studentList->next;
	if (ditStu != NULL)
	{
		while (ditStu != NULL)
		{
			if (ditStu->code == ditCode)
			{
				printf("请输入修改信息编号:\n1.姓名\n2.年龄\n3.数学\n4.语文\n5.英语\n");
				int number;
				scanf("%d", &number);
				switch (number)
				{
				case 1: changeName(ditStu);
					break;
				case 2: changeAge(ditStu);
					break;
				case 3:changeMathScore(ditStu);
					break;
				case 4:changeChineseScore(ditStu);
					break;
				case 5: changeEnglishScore(ditStu);
					break;
				default:
					printf("输入内容无效！");
				}
			}
			ditStu = ditStu->next;
		}
	}
	else {
		printf("抱歉，你还未录入学生信息，请先录入学生信息！\n");
	}
	printf("\t=========================\t\n");
	fenge();
}

//根据学生编号查找学生信息
void findStudent(Student* studentList)
{
	printf("请输入学号:");
	int code;
	scanf("%d", &code);
	Student* ditStu = studentList->next;
	if (ditStu != NULL)
	{
		while (ditStu != NULL)
		{
			if (ditStu->code != code)
			{
				ditStu = ditStu->next;
			}
			else {
				showMsg(ditStu);
				break;
			}
		}
	}
	else {
		printf("没有这名学生的信息！");
	}
	printf("\t=========================\t\n");
	fenge();
}


void showStudent(Student* studentList)
{
	Student* temp = studentList->next;
	printf("学号\t姓名\t年龄\t性别\t数学\t语文\t英语\n");
	while (temp != NULL) {
		showMsg(temp);
		temp = temp->next;
	}
	printf("\n");
	printf("\t=========================\t\n");
	fenge();

}



void saveStudent(Student* studentList)
{
	FILE* fp = NULL;
	fp = fopen("D:\\C\\studentMsg.txt", "a+");
	Student* stu = studentList->next;
	char title[N] = "学号\t姓名\t年龄\t性别\t数学\t语文\t英语\n";
	fprintf(fp, "%s", title);
	while (stu != NULL)
	{
		fprintf(fp, "%d\t%s\t%d\t%s\t%d\t%d\t%d\n", stu->code,
			stu->name, stu->age, stu->sex,stu->math, stu->chinese, stu->english);
		stu = stu->next;

	}
	fclose(fp);
	printf("\t=========================\t\n");
	fenge();
}


void showHelp()
{
	printf("1.此系统可以对学生信息进行管理。\n");
	printf("2.输入对应功能项的编号即可进行不同功能的系统操作。\N");
	printf("\t=========================\t\n");
	fenge();
}




void showMenu()
{
	int i;
	printf("----------------------------");
	printf("\t欢迎使用学生管理系统\t");
	printf("----------------------\n");
	printf("\t");
	for (i = 0;i < WIDESIZE;i++)
	{
		printf("*");

	}
	printf("\n");
	printf("\t*\t0.系统帮助及说明\t**");
	printf("\t1.刷新学生信息\t\t*\t\n");
	printf("\t*\t2.查询学生信息\t\t");
	printf("**\t3.修改学生信息\t\t*\n");
	printf("\t*\t4.增加学生信息\t\t**");
	printf("\t5.按学号删除信息\t*\n");
	printf("\t*\t6.显示所有学生信息\t**");
	printf("\t7.保存当前信息\t\t*\n");
	printf("\t*\t8.推出学生管理系统\t**");
	for (i = 0;i < 4;i++)
	{
		printf("\t");
	}
	printf("*\n");
	printf("\t");
	for (i = 0; i < WIDESIZE; i++)
	{
		printf("*");
	}
	printf("\n");
		printf("---------------------");
		printf("\t2020 xiaohai\t");
		printf("---------------------\n");
		printf("请按所需输入菜单编号:");
}





int main(int argc, char const* argv[])
{
	int choice;
	Student* studentList = createList();
	do
	{
		showMenu();
		scanf("%d", &choice);
		switch (choice)
		{
		case 0:showHelp();
			fenge();
			break;
		case 1:printf("刷新完成！\n");
			fenge();
			break;
		case 2:findStudent(studentList);
			fenge();
			break;
		case 3:editStudent(studentList);
			fenge();
			break;
		case 4:insertStudent(studentList);
			fenge();
			break;
		case 5:deleteStudent(studentList);
			fenge();
			break;
		case 6:showStudent(studentList);
			fenge();
			break;
		case 7:saveStudent(studentList);
			fenge();
			break;
		default:
			exit(1);
		}
	} while (1);
	return 0;
}
