{
#include <iostream>
#include <string>
#include <fstream>
using namespace std;

const int lenghtofstruct = 6;
const int lenghtofbookstruct = 5;
const int AmountofTop = 3;

struct Profile
{
	string fullName; 
	char sex;
	short int group;
	short int id;
	short int grades[8];
	short int library;
};

struct books
{
	string author;
	string bookname;
	short int year;
	short int NumberofPages;
	short int StudentNumber;
};

void creatingRecord() {
	while (true) {
		int temp = 0;
		Profile student;
		cout << "Please, print a fullName" << endl;
		if (!(cin >> student.fullName))
		{
			cout << "error" << endl;
			cin.clear();
			cin.ignore(numeric_limits<streamsize>::max(), '\n');
			break;
		}
		cout << "Please, print a sex (M/W)" << endl;
		if (!(cin >> student.sex))
		{
			cout << "error" << endl;
			cin.clear();
			cin.ignore(numeric_limits<streamsize>::max(), '\n');
			break;
		}
		cout << "Please, print a group" << endl;
		if (!(cin >> student.group && student.group >= 0 && student.group <= 1000000000))
		{
			cout << "error" << endl;
			cin.clear();
			cin.ignore(numeric_limits<streamsize>::max(), '\n');
			break;
		}
		cout << "Please, print an id" << endl;
		if (!(cin >> student.id && student.id >= 0 && student.id <= 1000000000))
		{
			cout << "error" << endl;
			cin.clear();
			cin.ignore(numeric_limits<streamsize>::max(), '\n');
			break;
		}
		for (int i = 0; i < 8; i++)
		{
			cout << "Please, print " << i << " grade" << endl;
			if (!(cin >> student.grades[i] && student.grades[i] >= 0 && student.grades[i] <= 5))
			{
				cout << "error" << endl;
				cin.clear();
				cin.ignore(numeric_limits<streamsize>::max(), '\n');
				break;
			}


		}
		cout << "Please, print a library card" << endl;
		if (!(cin >> student.library && student.library >= 0 && student.library <= 1000000000))
		{
			cout << "error" << endl;
			cin.clear();
			cin.ignore(numeric_limits<streamsize>::max(), '\n');
			break;
		}



		for (int i = 0; i < 8; i++)
		{
			if (student.grades[i] == 2)
				temp++;
		}
		if (temp == 0)
		{
			ofstream database;

			database.open("students.txt", ios::app);
			if (!database.is_open())
				cout << "Saving error!" << '\n';
			else
			{
				database << student.fullName << '\n';
				database << student.sex << '\n' << student.group << '\n' << student.id << '\n';
				for (int i = 0; i < 8; i++)
					database << student.grades[i] << " ";
				database << '\n';
				database << student.library << '\n';
				database.close();
				cout << endl;
				cout << "Profile is saved in the database." << '\n';
				cout << endl;
			}
		}
		else {
			cout << endl;
			cout << "This student will be expelled. The profile will not be saved in the database." << '\n';
			cout << endl;
		}
		break;
	}
}

void creatingBook() {
	while (true) {
		books book;
		cout << "Please, print a author" << endl;
		if (!(cin >> book.author))
		{
			cout << "error" << endl;
			cin.clear();
			cin.ignore(numeric_limits<streamsize>::max(), '\n');
			break;
		}
		cout << "Please, print a book name" << endl;
		if (!(cin >> book.bookname))
		{
			cout << "error" << endl;
			cin.clear();
			cin.ignore(numeric_limits<streamsize>::max(), '\n');
			break;
		}
		cout << "Please, print an year" << endl;
		if (!(cin >> book.year && book.year >= 0 && book.year <= 1000000000))
		{
			cout << "error" << endl;
			cin.clear();
			cin.ignore(numeric_limits<streamsize>::max(), '\n');
			break;
		}
		cout << "Please, print a number of pages" << endl;
		if (!(cin >> book.NumberofPages && book.NumberofPages >= 0 && book.NumberofPages <= 1000000000))
		{
			cout << "error" << endl;
			cin.clear();
			cin.ignore(numeric_limits<streamsize>::max(), '\n');
			break;
		}
		book.StudentNumber = 0;
			ofstream database;

			database.open("books.txt", ios::app);
			if (!database.is_open())
				cout << "Saving error!" << '\n';
			else
			{
				database << book.author << '\n';
				database << book.bookname << '\n' << book.year << '\n' << book.NumberofPages << '\n';
				database << book.StudentNumber << '\n';
				database.close();
				cout << endl;
				cout << "Profile is saved in the database." << '\n';
				cout << endl;
			}
		break;
	}
}

int countStudents() // Функция посчёта количества студентов
{
	ifstream database("students.txt");
	if (!database.is_open())
		cout << "Saving error!" << '\n';
	else
	{
		int temp = 0;
		string data;
		while (!database.eof())
		{
			getline(database, data);
			temp++;
		}
		database.close();
		int n;
		n = (temp-1) / lenghtofstruct;
		return n;
	}
	return 0;
}

int countBooks() // Функция посчёта количества студентов
{
	ifstream database("books.txt");
	if (!database.is_open())
		cout << "Saving error!" << '\n';
	else
	{
		int temp = 0;
		string data;
		while (!database.eof())
		{
			getline(database, data);
			temp++;
		}
		database.close();
		int n;
		n = (temp - 1) / lenghtofbookstruct;
		return n;
	}
	return 0;
}

void showData()
{
	ifstream database("students.txt");
	if (!database.is_open())
		cout << "File opening error";
	else
	{
		int temp;
		temp = countStudents();
		if (temp == 0)
			cout << "The File is empty";
		else
		{
			cout << endl;
			string data;
			int a;
			a = 0;
			while (a < (temp* lenghtofstruct))
			{
				switch (a% lenghtofstruct) {
				case 0:
					cout << "Student " << (a / lenghtofstruct)+1 << ":" << endl;
					cout << "Name: ";
					break;
				case 1:
					cout << "Sex: ";
					break;
				case 2:
					cout << "Group: ";
					break;
				case 3:
					cout << "Id: ";
					break;
				case 4:
					cout << "Grades: ";
					break;
				case 5:
					cout << "library card: ";
					break;
				}
				getline(database, data);

				cout << data << endl;
				if (a % lenghtofstruct == 5) {
					cout << endl;
				}
				a++;
			}
		}
		database.close();
	}
}

void showBook()
{
	ifstream database("books.txt");
	if (!database.is_open())
		cout << "File opening error";
	else
	{
		int temp;
		temp = countBooks();
		if (temp == 0)
			cout << "The File is empty";
		else
		{
			cout << endl;
			string data;
			int a;
			a = 0;
			while (a < (temp * lenghtofbookstruct))
			{
				switch (a % lenghtofbookstruct) {
				case 0:
					cout << "Book " << (a / lenghtofbookstruct) + 1 << ":" << endl;
					cout << "Author: ";
					break;
				case 1:
					cout << "Name: ";
					break;
				case 2:
					cout << "Year: ";
					break;
				case 3:
					cout << "Number of pages: ";
					break;
				case 4:
					cout << "Library card: ";
					break;
				}
				getline(database, data);

				cout << data << endl;
				if (a % lenghtofbookstruct == 4) {
					cout << endl;
				}
				a++;
			}
		}
		database.close();
	}
}

void showGroup()
{
	while (true) {
		int n; // Переменная, которая будет содержать информацию о введенном пользователем номере группы
		int size;
		cout << "Enter the group number:" << endl;
		if (!(cin >> n && n >= 0 && n <= 1000000000))
		{
			cout << "error" << endl;
			cin.clear();
			cin.ignore(numeric_limits<streamsize>::max(), '\n');
			break;
		}
		ifstream database("students.txt");
		if (!database.is_open())
			cout << "Error!";
		else
		{
			size = countStudents();
			if (size == 0)
				cout << "The database is empty." << endl;
			else
			{
				Profile* student = new Profile[size]; // В примере показан случай неопределенной размерности, от вас этого не требуется
				for (int i = 0; i < size; i++) // Считываем данные всех студентов в массив структур
				{
					database >> student[i].fullName;
					database >> student[i].sex >> student[i].group >> student[i].id;
					for (int j = 0; j < 8; j++)
						database >> student[i].grades[j];
					database >> student[i].library;
				}
				database.close(); // Закрываем файл
				int temp = 0;
				cout << endl;
				for (int i = 0; i < size; i++)
				{
					if (student[i].group == n)
					{
						cout << "Name: " << student[i].fullName << endl << "Sex: " << student[i].sex << endl;
						cout << "Group: " << student[i].group << endl;
						cout << "Id: " << student[i].id << endl;
						cout << "Grades: ";
						for (int j = 0; j < 8; j++)
							cout << student[i].grades[j] << " ";
						cout << "\n";
						cout << "library card: " << student[i].library << endl << endl;
						temp++;
					}
				}
				if (temp == 0)
					cout << "No records were found" << endl;
				cout << endl;
				delete[] student;
				
			}
		}
		break;
	}
}

void showId()
{
	while (true) {
		int n; // Переменная, которая будет содержать информацию о введенном пользователем номере группы
		int size;
		cout << "Enter the number in list:" << endl;
		if (!(cin >> n && n >= 0 && n <= 1000000000))
		{
			cout << "error" << endl;
			cin.clear();
			cin.ignore(numeric_limits<streamsize>::max(), '\n');
			break;
		}
		ifstream database("students.txt");
		if (!database.is_open())
			cout << "Error!";
		else
		{
			size = countStudents();
			if (size == 0)
				cout << "The database is empty." << endl;
			else
			{
				Profile* student = new Profile[size]; // В примере показан случай неопределенной размерности, от вас этого не требуется
				for (int i = 0; i < size; i++) // Считываем данные всех студентов в массив структур
				{
					database >> student[i].fullName;
					database >> student[i].sex >> student[i].group >> student[i].id;
					for (int j = 0; j < 8; j++)
						database >> student[i].grades[j];
					database >> student[i].library;
				}
				database.close(); // Закрываем файл
				int temp = 0;
				cout << endl;
				for (int i = 0; i < size; i++)
				{
					if (student[i].id == n)
					{
						cout << "Name: " << student[i].fullName << endl << "Sex: " << student[i].sex << endl;
						cout << "Group: " << student[i].group << endl;
						cout << "Id: " << student[i].id << endl;
						cout << "Grades: ";
						for (int j = 0; j < 8; j++)
							cout << student[i].grades[j] << " ";
						cout << "\n";
						cout << "library card: " << student[i].library << endl << endl;
						temp++;
					}
				}
				if (temp == 0)
					cout << "No records were found" << endl;
				cout << endl;
				delete[] student;

			}
		}
		break;
	}
}

void showAmountofSex()
{
	while (true) {
		int size;
		ifstream database("students.txt");
		if (!database.is_open())
			cout << "Error!";
		else
		{
			size = countStudents();
			if (size == 0)
				cout << "The database is empty." << endl;
			else
			{
				Profile* student = new Profile[size]; 
				for (int i = 0; i < size; i++) 
				{
					database >> student[i].fullName;
					database >> student[i].sex >> student[i].group >> student[i].id;
					for (int j = 0; j < 8; j++)
						database >> student[i].grades[j];
					database >> student[i].library;
				}
				database.close();
				int Man = 0;
				int Woman = 0;
				int Other = 0;
				cout << endl;
				for (int i = 0; i < size; i++)
				{
					if (student[i].sex == 'M')
						Man++;
					else
					{
						if (student[i].sex == 'W')
							Woman++;
						else
							Other++;
					}
				}
				cout << "Men: " << Man << endl;
				cout << "Women: " << Woman << endl;
				cout << "Undefined: " << Other << endl;
				cout << endl;

				delete[] student;

			}
		}
		break;
	}
}

void showTopofGrades() {
		int size;
		ifstream database("students.txt");
		if (!database.is_open())
			cout << "Error!";
		else
		{
			size = countStudents();
			if (size == 0)
				cout << "The database is empty." << endl;
			else
			{
				int topgrade[AmountofTop] = {};
				float mediumGradesMassive[AmountofTop] = {};
				float mediumGradeNew;
				Profile* student = new Profile[size];
				for (int i = 0; i < size; i++)
				{
					database >> student[i].fullName;
					database >> student[i].sex >> student[i].group >> student[i].id;
					for (int j = 0; j < 8; j++) {
						database >> student[i].grades[j];
					}
					database >> student[i].library;
				}
				database.close();
				cout << endl;

				for (int i = 0; i < size; i++)
				{
					mediumGradeNew = 0;
					for (int j = 0; j < 8; j++) {
						mediumGradeNew += student[i].grades[j];
					}
					mediumGradeNew /= 8;
					if (mediumGradesMassive[AmountofTop - 1] < mediumGradeNew) {
						for (int k = 0; k < AmountofTop; k++) {
							if ((mediumGradesMassive[AmountofTop - 1 - k] >= mediumGradeNew) && (k > 0)) {
								for (int j = 0; j < k; j++) {
									mediumGradesMassive[AmountofTop - 1 - j] = mediumGradesMassive[AmountofTop - 2 - j];
									topgrade[AmountofTop - 1 - j] = topgrade[AmountofTop - 2 - j];
								}
								mediumGradesMassive[AmountofTop - k] = mediumGradeNew;
								topgrade[AmountofTop - k] = i;
								break;
							}
							if ((mediumGradesMassive[AmountofTop - 1 - k] < mediumGradeNew) && (k == (AmountofTop - 1))) {
								for (int j = 0; j < k; j++) {
									mediumGradesMassive[AmountofTop - 1 - j] = mediumGradesMassive[AmountofTop - 2 - j];
									topgrade[AmountofTop - 1 - j] = topgrade[AmountofTop - 2 - j];
								}
								mediumGradesMassive[AmountofTop - 1 - k] = mediumGradeNew;
								topgrade[AmountofTop - 1 - k] = i;
								break;
							}
						}
					}
				}
				for (int i = 0; i < AmountofTop; i++) {
					cout << student[topgrade[i]].fullName << " from " << student[topgrade[i]].group << " group has " << mediumGradesMassive[i] << " GPA" << endl;
				}

				cout << endl;

				delete[] student;

			}
		}
}

void showbyGrade() {
	while (true) {
		int n; // Переменная, которая будет содержать информацию о введенном пользователем номере группы
		int size;
		cout << "1 - only great, 2 - only good and great, 3 - without scholarship" << endl;
		if (!(cin >> n && n >= 1 && n <= 3))
		{
			cout << "error" << endl;
			cin.clear();
			cin.ignore(numeric_limits<streamsize>::max(), '\n');
			break;
		}
		ifstream database("students.txt");
		if (!database.is_open())
			cout << "Error!";
		else
		{
			size = countStudents();
			if (size == 0)
				cout << "The database is empty." << endl;
			else
			{
				Profile* student = new Profile[size]; // В примере показан случай неопределенной размерности, от вас этого не требуется
				for (int i = 0; i < size; i++) // Считываем данные всех студентов в массив структур
				{
					database >> student[i].fullName;
					database >> student[i].sex >> student[i].group >> student[i].id;
					for (int j = 0; j < 8; j++)
						database >> student[i].grades[j];
					database >> student[i].library;
				}
				database.close(); // Закрываем файл
				int temp = 0;
				int brak = 0;
				int countFourandThree = 0;
				cout << endl;
				for (int i = 0; i < size; i++)
				{
					switch (n) {

					case 1:
						for (int j = 0; j < 8; j++) {
							if (student[i].grades[j] != 5) {
								brak = 1;
								break;
							}
						}
						if (brak == 1) {
							brak = 0;
							break;
						}
						cout << "Name: " << student[i].fullName << endl << "Sex: " << student[i].sex << endl;
						cout << "Group: " << student[i].group << endl;
						cout << "Id: " << student[i].id << endl;
						cout << "Grades: ";
						for (int j = 0; j < 8; j++)
							cout << student[i].grades[j] << " ";
						cout << "\n";
						cout << "library card: " << student[i].library << endl << endl;
						temp++;
						break;
					case 2:
						countFourandThree = 0;
						for (int j = 0; j < 8; j++) {
							if (student[i].grades[j] < 4) {
								brak = 1;
								break;
							}
							if (student[i].grades[j] == 4)
								countFourandThree++;
						}
						if (brak == 1) {
							brak = 0;
							break;
						}
						if (countFourandThree > 0) {
							cout << "Name: " << student[i].fullName << endl << "Sex: " << student[i].sex << endl;
							cout << "Group: " << student[i].group << endl;
							cout << "Id: " << student[i].id << endl;
							cout << "Grades: ";
							for (int j = 0; j < 8; j++)
								cout << student[i].grades[j] << " ";
							cout << "\n";
							cout << "library card: " << student[i].library << endl << endl;
							temp++;
						}
						break;
					case 3:
						countFourandThree = 0;
						for (int j = 0; j < 8; j++) {
							if (student[i].grades[j] < 3) {
								brak = 1;
								break;
							}
							if (student[i].grades[j] == 3)
								countFourandThree++;
						}
						if (brak == 1) {
							brak = 0;
							break;
						}
						if (countFourandThree > 0) {
							cout << "Name: " << student[i].fullName << endl << "Sex: " << student[i].sex << endl;
							cout << "Group: " << student[i].group << endl;
							cout << "Id: " << student[i].id << endl;
							cout << "Grades: ";
							for (int j = 0; j < 8; j++)
								cout << student[i].grades[j] << " ";
							cout << "\n";
							cout << "library card: " << student[i].library << endl << endl;
							temp++;
						}
						break;
					}
					
				}
				if (temp == 0) {
					cout << endl;
					cout << "No records were found" << endl;
				}
				cout << endl;
				delete[] student;

			}
		}
		break;
	}
}

void changeStudent() {
	while (true) {
		int what;
		int group;
		int NumberofList;
		int size;
		int contin;
		cout << "Enter the group number:" << endl;
		if (!(cin >> group && group >= 0 && group <= 1000000000))
		{
			cout << "error" << endl;
			cin.clear();
			cin.ignore(numeric_limits<streamsize>::max(), '\n');
			break;
		}
		cout << "Enter the id:" << endl;
		if (!(cin >> NumberofList && NumberofList >= 0 && NumberofList <= 1000000000))
		{
			cout << "error" << endl;
			cin.clear();
			cin.ignore(numeric_limits<streamsize>::max(), '\n');
			break;
		}
		ifstream database("students.txt");
		if (!database.is_open())
			cout << "Error!";
		else
		{
			size = countStudents();
			if (size == 0)
				cout << "The database is empty." << endl;
			else
			{
				Profile* student = new Profile[size]; // В примере показан случай неопределенной размерности, от вас этого не требуется
				for (int i = 0; i < size; i++) // Считываем данные всех студентов в массив структур
				{
					database >> student[i].fullName;
					database >> student[i].sex >> student[i].group >> student[i].id;
					for (int j = 0; j < 8; j++)
						database >> student[i].grades[j];
					database >> student[i].library;
				}
				database.close(); // Закрываем файл
				int temp = 0;
				cout << endl;
				for (int i = 0; i < size; i++)
				{
					if (student[i].group == group)
					{
						if (student[i].id == NumberofList)
						{
							while (true) {
								cout << "Name: " << student[i].fullName << endl << "Sex: " << student[i].sex << endl;
								cout << "Group: " << student[i].group << endl;
								cout << "Id: " << student[i].id << endl;
								cout << "Grades: ";
								for (int j = 0; j < 8; j++)
									cout << student[i].grades[j] << " ";
								cout << "\n";
								cout << "library card: " << student[i].library << endl << endl;
								temp++;
								cout << "What do you want to change there?" << endl;
								cout << "0 - nothing" << endl;
								cout << "1 - Name" << endl;
								cout << "2 - Sex" << endl;
								cout << "3 - Group" << endl;
								cout << "4 - id" << endl;
								cout << "5 - Grades" << endl;
								cout << "6 - library card" << endl;
								if (!(cin >> what && what >= 0 && what <= 6))
								{
									cout << "error" << endl;
									cin.clear();
									cin.ignore(numeric_limits<streamsize>::max(), '\n');
									break;
								}
								switch (what) {
								case 0:
									break;
								case 1:
									cout << "Please, print a fullName" << endl;
									if (!(cin >> student[i].fullName))
									{
										cout << "error" << endl;
										cin.clear();
										cin.ignore(numeric_limits<streamsize>::max(), '\n');
										break;
									}
									break;
								case 2:
									cout << "Please, print a Sex (M/W)" << endl;
									if (!(cin >> student[i].sex))
									{
										cout << "error" << endl;
										cin.clear();
										cin.ignore(numeric_limits<streamsize>::max(), '\n');
										break;
									}
									break;
								case 3:
									cout << "Please, print a group" << endl;
									if (!(cin >> student[i].group && student[i].group >= 0 && student[i].group <= 1000000000))
									{
										cout << "error" << endl;
										cin.clear();
										cin.ignore(numeric_limits<streamsize>::max(), '\n');
										break;
									}
									break;
								case 4:
									cout << "Please, print an id" << endl;
									if (!(cin >> student[i].id && student[i].id >= 0 && student[i].id <= 1000000000))
									{
										cout << "error" << endl;
										cin.clear();
										cin.ignore(numeric_limits<streamsize>::max(), '\n');
										break;
									}
									break;
								case 5:
									for (int j = 0; j < 8; j++)
									{
										cout << "Please, print " << j << " grade" << endl;
										if (!(cin >> student[i].grades[j] && student[i].grades[j] >= 0 && student[i].grades[j] <= 5))
										{
											cout << "error" << endl;
											cin.clear();
											cin.ignore(numeric_limits<streamsize>::max(), '\n');
											break;
										}


									}
									break;
								case 6:
									cout << "Please, print a library card" << endl;
									if (!(cin >> student[i].library && student[i].library >= 0 && student[i].library <= 1000000000))
									{
										cout << "error" << endl;
										cin.clear();
										cin.ignore(numeric_limits<streamsize>::max(), '\n');
										break;
									}
								}
								cout << "Something else? (1 - yes, 0 - no)" << endl;
								if (!(cin >> contin && contin >= 0 && contin <= 1))
								{
									cout << "error" << endl;
									cin.clear();
									cin.ignore(numeric_limits<streamsize>::max(), '\n');
									break;
								}
								if (contin == 0)
									break;
							}
						}
					}
				}
				if (remove("students.txt")) {
					printf("Error removing file");
					break;
				}
				ofstream database;

				database.open("students.txt", ios::app);
				if (!database.is_open())
					cout << "Saving error!" << '\n';
				else
				{
					for (int i = 0; i < size; i++) {
						database << student[i].fullName << '\n';
						database << student[i].sex << '\n' << student[i].group << '\n' << student[i].id << '\n';
						for (int j = 0; j < 8; j++)
							database << student[i].grades[j] << " ";
						database << '\n';
						database << student[i].library << '\n';
					}
					database.close();
					cout << endl;
					cout << "Profile is saved in the database." << '\n';
					cout << endl;
				}
				if (temp == 0) {
					cout << endl;
					cout << "No records were found" << endl;
					cout << endl;
				}
				delete[] student;

			}
		}
		break;
	}
}

void gotoLibrary() {
		while (true) {
			int what;
			string bookname;
			int size;
			int contin;
			short int whatare;
			cout << "What are you doing? (1 - pick a book, 2 - return a book)" << endl;
			if (!(cin >> whatare && whatare >= 1 && whatare <= 2))
			{
				cout << "error" << endl;
				cin.clear();
				cin.ignore(numeric_limits<streamsize>::max(), '\n');
				break;
			}
			cout << "Enter the book name:" << endl;
			if (!(cin >> bookname))
			{
				cout << "error" << endl;
				cin.clear();
				cin.ignore(numeric_limits<streamsize>::max(), '\n');
				break;
			}
			ifstream database("books.txt");
			if (!database.is_open())
				cout << "Error!";
			else
			{
				size = countBooks();
				if (size == 0)
					cout << "The database is empty." << endl;
				else
				{
					books* book = new books[size]; // В примере показан случай неопределенной размерности, от вас этого не требуется
					for (int i = 0; i < size; i++) // Считываем данные всех студентов в массив структур
					{
						database >> book[i].author;
						database >> book[i].bookname >> book[i].year >> book[i].NumberofPages;
						database >> book[i].StudentNumber;
					}
					database.close(); // Закрываем файл
					int temp = 0;
					cout << endl;
					for (int i = 0; i < size; i++)
					{
						if (book[i].bookname == bookname && ((whatare==2 && book[i].StudentNumber>0) || (whatare == 1 && book[i].StudentNumber == 0)))
						{
							cout << "Author: " << book[i].author << endl << "Name: " << book[i].bookname << endl;
							cout << "Year: " << book[i].year << endl;
							cout << "Number of pages: " << book[i].NumberofPages << endl;
							cout << "library card: " << book[i].StudentNumber << endl << endl;
							temp++;
							cout << "Is that right book? (1 - yes, 0 - no)" << endl;
							if (!(cin >> contin && contin >= 0 && contin <= 1))
							{
								cout << "error" << endl;
								cin.clear();
								cin.ignore(numeric_limits<streamsize>::max(), '\n');
								break;
							}
							if (contin == 0)
								continue;
							int student = 0;
							if (whatare == 1) {
								cout << "What is student`s library card?" << endl;
								if (!(cin >> student && student >= 0 && student <= 1000000))
								{
									cout << "error" << endl;
									cin.clear();
									cin.ignore(numeric_limits<streamsize>::max(), '\n');
									break;
								}
							}
							book[i].StudentNumber = student;
						}
					}
					if (temp > 0) {
						if (remove("books.txt")) {
							printf("Error removing file");
							break;
						}
						ofstream database;

						database.open("books.txt", ios::app);
						if (!database.is_open())
							cout << "Saving error!" << '\n';
						else
						{
							for (int i = 0; i < size; i++) {
								database << book[i].author << '\n';
								database << book[i].bookname << '\n' << book[i].year << '\n' << book[i].NumberofPages << '\n';
								database << book[i].StudentNumber << '\n';
							}
							database.close();
							cout << endl;
							cout << "Profile is saved in the database." << '\n';
						}
					}
					if (temp == 0)
						cout << endl;
						cout << "No records were found" << endl;
					delete[] book;
					cout << endl;

				}
			}
			break;
		}
}

int main()
{
	while (true) {
		short int task;



		cout << "Please, print a number of task:" << endl;
		cout << "0 - close programm:" << endl;
		cout << "1 - creat new record" << endl;
		cout << "2 - change one record" << endl;
		cout << "3 - show all data" << endl;
		cout << "4 - show all data of one group" << endl;
		cout << "5 - show best students" << endl;
		cout << "6 - count male and female" << endl;
		cout << "7 - show students by grade" << endl;
		cout << "8 - show all data of id" << endl;
		cout << "9 - create new book" << endl;
		cout << "10 - go to library" << endl;
		cout << "11 - show all books" << endl;
		if (!(cin >> task && task >= 0 && task <= 11))
		{
			cout << "error" << endl;
			cin.clear();
			cin.ignore(numeric_limits<streamsize>::max(), '\n');
			task = -1;
		}
		switch (task)
		{
		case 0:
			goto exit;
		case 1:
			creatingRecord();
			break;
		case 2:
			changeStudent();
			break;
		case 3:
			showData();
			break;
		case 4:
			showGroup();
			break;
		case 5:
			showTopofGrades();
			break;
		case 6:
			showAmountofSex();
			break;
		case 7:
			showbyGrade();
			break;
		case 8:
			showId();
			break;
		case 9:
			creatingBook();
			break;
		case 10:
			gotoLibrary();
			break;
		case 11:
			showBook();
			break;
		}
	}
	exit:
	return 0;
}
}
