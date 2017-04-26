#include<iostream>
#include<string>
using namespace std;

enum Tsex{mid,man,woman};
struct course {
	string coursename;
	int grade;
};

class Person {
	string IdPerson;
	string Name;
	Tsex Sex;
	int Birthday;
	string HomeAddress;
public:
	Person(string, string, Tsex, int, string);
	Person();
	~Person();
	void SetName(string);
	string GetName() { return Name; }
	void SetSex(Tsex sex) { Sex = sex; }
	Tsex GetSex() { return Sex; }
	void SexId(string id) { IdPerson = id; }
	string GetId() { return IdPerson; }
	void SetBirth(int birthday) { Birthday = birthday; }
	int GetBirth() { return Birthday; }
	void SetHomeAdd(string);
	string GetHomeAdd() { return HomeAddress; }
	void PrintPersonInfo();
};

Person::Person(string id, string name, Tsex sex, int birthday, string homeadd)
{
	IdPerson = id;
	Name = name;
	Sex = sex;
	Birthday = birthday;
	HomeAddress = homeadd;
}

Person::Person()
{
	IdPerson = "#"; Name = "#"; Sex = mid;
	Birthday = 0; HomeAddress = "#";
}

Person::~Person(){}

void Person::SetName(string name)
{
	Name = name;
}

void Person::SetHomeAdd(string homeadd)
{
	HomeAddress = homeadd;
}

void Person::PrintPersonInfo()
{
	int i;
	cout << "身份账号：" << IdPerson << '\n' << "姓名：" << Name << '\n' << "性别：";
	if (Sex == man)cout << "男" << '\n';
	else if (Sex == woman)cout << "女" << '\n';
		else cout << "" << '\n';
	cout << "出生年月日：";
	i = Birthday;
	cout << i / 10000 << "年";
	i = i % 10000;
	cout << i / 100 << "月" << i % 100 << "日" << '\n' << "家庭地址：" << HomeAddress << '\n';
}
  
class Student:public Person {
	string NoStudent;
	course cs[30];
public:
	Student(string id, string name, Tsex sex, int birthday, string homeadd, string nostud);
	Student();
	~Student();
	int SetCourse(string, int);
	int GetCourse(string);
	void PrintStudentIbfo();
};

Student::Student(string id, string name, Tsex sex, int birthday, string homeadd, string nostud)
	:Person(id,name,sex,birthday,homeadd)
{
	int i; NoStudent = nostud;
	for(i=0;i<30;i++)
	{
		cs[i].coursename = "#";
		cs[i].grade = 0;
	}
}

Student::Student()
{
	int i;
	NoStudent = "0";
	for(i=0;i<30;i++)
	{
		cs[i].coursename = "#";
		cs[i].grade = 0;
	}
}

Student::~Student(){ }

int Student::SetCourse(string coursename, int grade)
{
	int i;
	bool b = false;
	for(i=0;i<30;i++)
	{
		if (cs[i].coursename == "#")
		{
			cs[i].coursename = coursename;
			cs[i].grade = grade;
			b = false;
			break;
		}
		else if (cs[i].coursename == coursename)
		{
			cs[i].grade = grade;
			b = true;
			break;
		}
	}
	if (i == 30)return 0;
	if (b)return 1;
	else return 2;
}

int Student::GetCourse(string coursename)
{
	int i;
	for (i = 0; i < 30; i++)if (cs[i].coursename == coursename)return cs[i].grade;
	return -1;
}

void Student::PrintStudentIbfo()
{
	int i;
	cout << "学号：" << NoStudent << '\n';
	PrintPersonInfo();
	for (i = 0; i < 30; i++)
	{
		if (cs[i].coursename != "#")cout << cs[i].coursename << '\t' << cs[i].grade << '\n';
		else break;
	}
	cout << "--------完--------" << endl;
}

int main(void)
{
	char temp[30];
	int i, k;
	Person per1("3201012820818161", "沈俊", man, 19820818, "南京市四牌楼2号");
	Person per2;
	per2.SetName("朱明");
	per2.SetSex(woman);
	per2.SetBirth(19780528);
	per2.SexId("320102780528162");
	per2.SetHomeAdd("南京市成贤街9号");
	per1.PrintPersonInfo();
	per2.PrintPersonInfo();
	Student stu1("320102811226161", "朱海鹏", man, 19811226, "南京市黄浦路1号", "06000123");
	cout << "请输入各科成绩：" << '\n';
	while (1)
	{
		cin >> temp;
		if (!strcmp(temp, "end"))break;
		cin >> k;
		i = stu1.SetCourse(temp, k);
		if (i == 0)cout << "成绩列表已满！" << '\n';
		else if (i == 1)cout << "修改成绩" << '\n';
			 else cout << "登记成绩" << '\n';
	}
	stu1.PrintStudentIbfo();
	while (1)
	{
		cout << "查询成绩" << '\n' << "请输入科目" << '\n';
		cin >> temp;
		if (!strcmp(temp, "end"))break;
		k = stu1.GetCourse(temp);
		if (k == -1)cout << "未查到" << '\n';
		else cout << k << '\n';
	}
	return 0;
}
