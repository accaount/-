# -1.	Дано целое число N и массив из N целых чисел, содержащий по крайней мере 2 нуля. Вывести сумму чисел из этого массива, расположенных между последними 2 нулями. Если они идут подряд, то вывести 0.
#include <iostream>
void filling(int const& N, int& zero1, int& zero2, int* A)
{
	bool flag = 0; //Создаём флаг, чтобы понимать, где первый ноль, а где последний
	for (int i = 0; i < N; i++)
	{
		scanf(A[i]);
		if (!A[i] && flag) //Если A[i] == 0 и флаг равен истине
		{
			zero1 = i; //Запоминаем индекс от первого нуля
			flag = false; //Флаг меняем на ложь, чтобы следующий индекс нуля присваивался ко второму индексу(izero2)
		}
		else if (!A[i]) //Если A[i] == 0
		{
			zero2 = i; //Запоминаем индекс от второго нуля
			flag = true; //Флаг меняем на истину, чтобы следующий индекс нуля присваивался к первому индексу(izero1)
		}
	}
}
int operation(int& zero1, int& zero2, int* A)
{
	int s = 0;
	if (zero1 < zero2) //Если номер первого индекса меньше второго, то считаемследующим циклом :
		for (zero1++; zero1 < zero2; zero1++)
			s += A[zero1]; //Считаем сумму
	else //Если номер второго индекса меньше первого, то считаем следующим циклом:
		for (zero2++; zero2 < zero1; zero2++)
			s += A[zero2]; //Считаем сумму
	return s;
}
int main()
{
	int N, izero1 = 0, izero2 = 0;
	int A[255] = { 0 };
	scanf(N);
	filling(N, izero1, izero2, A);
	printf(operation(izero1, izero2, A));
	system("pause");
}

2.	Вычислить сумму элементов матрицы в тех строках, которые содержат положительные, отрицательные и нулевые элементы.
#include <iostream>
void filling(int& m, int& n, int** A) //Заполняем матрицу
{
	for (int i = 0; i < m; i++)
		A[i] = new int[n];
	for (int i = 0; i < m; i++)
		for (int j = 0; j < n; j++)
			scanf(A[i][j]);
}
void operation(int& m, int& n, int** A)
{
	for (int i = 0; i < m; i++)
	{
		bool q1 = false, q2 = false, q3 = false; //Создаём "флаги" для определения условий,которые выполняются у нас в строке
			int s = 0;
		for (int j = 0; j < n; j++)
		{
			if (A[i][j] > 0)
			{
				s += A[i][j];
				q1 = true; //Флаг, отвечающий за положительные числа
			}
			else if (A[i][j] < 0)
			{
				s += A[i][j];
				q2 = true; //Флаг, отвечающий за отрицательные числа
			}
			else if (A[i][j] == 0)
			{
				q3 = true; //Флаг, отвечающий за нулевые числа
			}
		}
		if (q1 && q2 && q3) printf(s); //Если все три флага равны истине, то выводим сумму элементов в строке
		else printf ("Строка не подходит по условию"; //Иначе выводим соответсвующее сообщение
	}
}
int main()
{
	setlocale(LC_ALL, "Russian");
	int m, n;
	int** A;
	scanf(m, n);
	A = new int* [m];
	filling(m, n, A);
	operation(m, n, A);
	system("pause");
}

3.	Дан массив размера N. Найти номер максимального из его локальных минимумов (локальный минимум – элемент, который меньше любого из своих соседей)
#include <iostream>
using namespace std;
void operation(int& N, int* A)
{
	int index = 0;
	for (int i = 0; i < N; i++) scanf(A[i]); //Заполняем массив
	int max = A[0]; //Задаём за максимальный локальный минимум самый первый элемент массива, чтобы сравнить его с другими
		for (int i = 1; i < N - 1; i++)
		{
			if (A[i] < A[i - 1] && A[i] < A[i + 1] && A[i] > max)
			{
				max = A[i]; //Меняем максимальный локальный минимум на новое значение
				index = i; //Запоминаем его индекс
			}
		}
	if (A[N - 1] < A[N - 2] && A[N - 1] > max) index = N - 1; //Определяем, является ли максимальным локальным минимумом последнее число
		printf(index + 1); //Выводим последовательный номер элемента (не егоиндекс)
}
int main()
{
	int N;
	int* A;
	scanf(N);
	A = new int[N];
	operation(N, A);
	system("pause");
}


4. Ввести с клавиатуры строку. Определить количество слов в строке между словами максимальной и минимальной длины
#include <iostream>
using namespace std;
#define N 100
void function(char s[N])
{
	int word = 0, min = 100, max = 0, imin = 0, imax = 0, sum = 0, j1 = 0, j2 = 0;
	for (int i = 0; i < strlen(s) + 1; i++)
	{
		if ((s[i] == '\0') && (word == 0)) break; //поиск конца строки и остановка
		if ((s[i] != ' ') && (s[i] != '\0')) word++; //подсчет букв в слове
		else
		{ //сравнивание с максимальной и минимальной длиной слова
			if (word > max) { max = word; imax = i; }
			if (word < min) { min = word; imin = i; }
			word = 0;
		}
	}
	if (imax > imin) { j2 = (imax - max); j1 = imin; }
	//определяет, какое слово стоит раньше, записывает индексы для подсчета суммы
	else { j2 = (imin - min); j1 = imax; }
	for (int i = j1; i < j2; i++)
		if (s[i] == ' ') sum++; //считает количество пробелов
	printf("количество слов:", sum - 1); //количество слов = пробелы-1
}
int main()
{
	setlocale(LC_ALL, "Russian");
	printf("Введите преддложение");
	char s[N] = { 0 };
	gets_s(s, N);
	function(s);
	system("pause");
	return 0;
}

5.Ввести с клавиатуры строку. Вывести на экран все слова, начинающиеся и заканчивающиеся на одну и ту же букву.
#include <iostream>
#include <cstring>
using namespace std;
void operation(char* s)
{
    int word = 0;
    for (int i = 0; i <= strlen(s); i++)
    {
        if ((s[i] == '\0') && (word == 0))// находит конец предложения
            break;
        else if ((s[i] != ' ') && (s[i] != '\0'))//находит пробел между словами
            word++;//считает длину слова
        else
        {
            if (s[i - 1] == s[i - word]) //сравнивает первую и последнюю букву
            {
                for (int j = i - word; j < i; j++)
                    printf(s[j]); //выписывает слово
                printf(' ');
            }
            word = 0;
        }
    }
    printf("\n");
}
int main()
{
    char s[255] = { 0 };
    printf("Введите строку:\n ");
    gets_s(s);
    operation(s);
    system("pause");
}

6.Вычислить произведение элементов массива, расположенных между первым положительным и последним отрицательным числом.
#include <iostream>
using namespace std;
void filling(int& N, int& iplus, int& iminus, int* A)
{
	for (int i = 0; i < N; i++)
	{
		scanf(A[i]);
		if (A[i] > 0 & iplus == -1)
			iplus = i; //Запоминаем индекс от крайнего слева положительного
		if (A[i] < 0)
			iminus = i; //Запоминаем индекс от крайнего справа отрицательного
	}
}
int operation(int& iplus, int& iminus, int* A)
{
	int s = 1;
	if (iplus < iminus) //Если номер первого индекса меньше второго, то считаемследующим циклом :
	for (iplus++; iplus < iminus; iplus++)
		s *= A[iplus]; //Считаем произведение
	else //Если номер второго индекса меньше первого, то считаем следующим циклом:
		for (iminus++; iminus < iplus; iminus++)
			s *= A[iminus]; //Считаем произведение
	return s; //Выводим произведение
}
int main()
{
	int N, iplus = -1, iminus = 0;
	int A[255] = { 0 };
	scanf(N);
	filling(N, iplus, iminus, A);
	printf( operation(iplus, iminus, A));
	system("pause");
}
7. Даны 2 массива целых чисел a и b. Массив а отсортирован по возрастанию. Вставить в массив а элементы массивы b так, чтобы он остался отсортирован.
#include <iostream>
using namespace std;
int humain(int a[10], int b[5])
{
	int i, j, t;
	for (i = 0; i < 5; i++)
	{
		for (j = 0; j < 10; j++)
		{
			if ((b[i] < a[j]) || (b[i] == a[j])) //сравнивание элементов двух массивов
			{
				for (t = 10; t > j; t--) { a[t] = a[t - 1]; }
				a[j] = b[i]; //Вставляем из б в а по возрастанию
				break;
			}
			if ((j > 4) & (a[j] == 0)) { a[j] = b[i]; break; }
		}
	}
	printf("отсортированный по возрастанию массив a: ");;
	for (i = 0; i < 10; i++)
	{
		printf(a[i]," ");
	}
	return 0;
}
int main()
{
	setlocale(LC_ALL, "Russian");
	int a[11] = { 0 }, b[5];
	printf("Введите отсортированный по возрастанию массив a: ");
	for (int i = 0; i < 5; i++) { scanf( a[i]); }
	printf("Введите массив b: ");
	for (int i = 0; i < 5; i++) { scanf(b[i]); }
	humain(a, b);
	return 0;
}
8. Определить количество отрицательных элементов в тех строках матрицы, которые содержат хотя бы 1 нулевой элемент. 
#include <iostream>
using namespace std;
void AFA()
{
    int a = 0;
    int sum[3];
    int string[3];
    int x[3][4] = { {2, 7, 4, 0 },
                    {3, 0, -5, -6},
                    {4, -5, 0, 7} };//инициализация матрицы
    for (int i = 0; i < 3; i++)
    {
        string[i] = 0;
    }
    for (int i = 0; i < 3; i++)
    {
        sum[i] = 0;
    }
    for (int i = 0; i < 3; i++)   //вывод матрицы               
    {
        for (int j = 0; j < 4; j++)
        {
            printf(x[i][j], " ");
        }
        printf('\n');
    }
    for (int i = 0; i < 3; i++) {//Находим нули в матрице и запоминаем строчки
        for (int j = 0; j < 4; j++)
        {
            if (x[i][j] == 0)
            {
                string[i] = string[i] + 1;
            }
        }
    }
    for (int i = 0; i < 3; i++) //Находим отрицательные илименты в строках которые запомнили и считаим их количество
    {
        if (string[i] > 0)
        {
            a = i;
            for (int j = 0; j < 4; j++)
            {
                if (x[a][j] < 0)
                {
                    sum[a] = sum[a] + 1;
                }
            }
        }
    }
    for (int i = 0; i < 3; i++)
    {//Выводим строки количество отрицательных элементов в каждой строке матрицы
        if (sum[i] > 0)
        {
            printf("Колическтво отрицательных элементов в строке " , i , " равно: ", sum[i]);
        }
    }
    for (int i = 0; i < 3; i++)
    {
        if (sum[i] == 0)
        {
            printf("Строка " , i , " не имеет отрицательных элементов"); 
        }
    }
}
int main()
{
    setlocale(LC_ALL, "rus");
    AFA();
    system("pause");
}

9.Сжать массив целых чисел, удалив из него нулевые элементы.
#include <iostream>
using namespace std;
void operation(int& N, int* A)
{
	for (int i = 0; i < N; i++) scanf(A[i]); //Заполняем массив
	for (int i = 0; i < N; i++)
		if (!A[i]) //Если A[i] == 0
		{
			for (int j = i; j < N; j++) A[j] = A[j + 1]; //Сдвигаем массив влево, удаляя нулевойэлемент
				A[N] = 0; //Массив сдвинут на один элемент влево, удалим последний элемент
			N--; //Массив сжали - размер уменьшился
			i--; //Сдвигаем по циклу на шаг назад, так как массив сдвинулся
		}
	for (int i = 0; i < N; i++) cout << A[i] << ' '; //Выводим элементы массива
}
int main()
{
	int N;
	int* A;
	scanf(N);
	A = new int[N];
	operation(N, A);
	system("pause");
}
10. Посчитать сумму элементов массива до последнего положительного элемента.
#include <iostream>
#define N 10
void function(int a[N])
{
	int j = 0, sum = 0;
	for (int i = N - 1; i >= 0; i--)
		if (a[i] > 0) { j = i; break; } //поиск последнего положительного 
	if (j != 0) //подсчет суммы
	{
		for (int i = 0; i < j; i++)
			sum += a[i];
		printf("Сумма:", sum);
	} //случай если положительных нет или он стоит первым
	else printf("Положительных элементов нет, или он стоит первым.");
}
int main()
{
	setlocale(LC_ALL, "Russian");
	int a[N];
	printf("Введите массив");
	for (int i = 0; i < N; i++)
	{
		scanf_s("%d",a[i]);
	}
	function(a);
	system("pause");
	return 0;
}

11. Дан целочисленный массив размера N. Посчитать чередуются ли в нем четные и нечетные числа. Если чередуются, то вывести 0, если нет, то порядковый номер элемента, нарушающего закономерность.

#include <iostream>
using namespace std;
int operation(int &N, int *A)
{
int s = 0;
bool flag; //Создаём флаг для определения какой элемент был предыдущим
for (int i = 0; i < N; i++) cin >> A[i]; //Заполняем массив
A[0] % 2 ? flag = true : flag = false; //Смотрим, является ли чётным самое первое
число
for (int i = 0; i < N; i++)
{
if (!(A[i] % 2) && !flag) flag = true; //Если A[i] чётное и флаг был нечётным, то флаг
меняем на чётное
else if (A[i] % 2 && flag) flag = false; //Если A[i] нечётное и флаг был чётным, то
флаг меняем на нечётное
else //Иной случай говорит нам о том, что чередование нарушено
{
s = i + 1; //Нужно найти порядковый номер, поэтому к индексу добавляем 1
break; //Выходим из цикла, так как мы нашли элемент, нарушающий
чередование
}
}
return s; //Выводим порядковый номер
}
int main()
{
int N;
int *A;
cin >> N;
A = new int [N];
cout << operation(N, A) << endl;
system("pause");
}
12. Ввести с клавиатуры строку. Определить количество слов, в которых ни одна буква
не повторяется.
#include <iostream>
#include <cstring>
using namespace std;
bool unique(char *s, int const &i, int const &word)
{
for (int k = i - word; k < i - 1; k++) //Прогоняем слово начиная от первой буквы и
заканчивая предпоследней
for (int l = k + 1; l < i; l++) //Прогоняем со второй буквы, заканчивая последней
if (s[k] == s[l]) //Если есть совпадения, то немедленно возвращаем ложь
return false;
return true; //Если совпадений не было, то возвращаем истину
}
void operation(char *s)
{
int word = 0;
int count = 0;
for (int i = 0; i <= strlen(s); i++) //Пробегаем через всю строку (включая
нуль-терминатор)
{
if ((s[i] == '\0') && (word == 0)) //Если встретили нуль-терминатор и проделали все
операции (word = 0), то выходим из цикла
break;
else if ((s[i] != ' ') && (s[i] != '\0')) //Считаем количество букв в слове
word++;
else
{
if (unique(s, i, word)) count += 1; //Проверяем, не повторяются ли в слове буквы,
если нет, то добавляем к счётчику единицу
word = 0; //Переходим к другому слову, обнуляем количество букв
}
}
cout << count << endl; //Выводим количество
}
int main()
{
char s[255] = {0};
gets(s);
operation(s);
system("pause");
}
13. Ввести с клавиатуры строку, состоящую из слов, разделенных пробелов, точкой и
запятой. Если в словах встречается окончание ing, заменить его на ed.
#include <iostream>
#include <cstring>
using namespace std;
void operation(char *s)
{
for (int i = 0; i <= strlen(s); i++) //Пробегаем через всю строку (включая
нуль-терминатор)
{
if (s[i - 1] == 'g' && s[i - 2] == 'n' && s[i - 3] == 'i') //Если слово оканчивается на ing
{
for (int k = i - 1; k < strlen(s); k++) s[k] = s[k + 1]; //То сдвигаем массив влево на
один элемент
s[i - 2] = 'd'; //Последние две буквы меняем на нужное окончание
s[i - 3] = 'e';
}
}
}
int main()
{
char s[255] = {0};
gets(s);
operation(s);
puts(s);
system("pause");
}
14. Даны 2 целых и положительных числа А и В. Написать программу, которая
выводит сумму чисел между А и В, причем каждое число выводится столько раз,
сколько значению оно равно (например число 3 выводится 3 раза).
#include <iostream>
using namespace std;
void operation(int &A, int &B)
{
if (B < A) A = A + B - (B = A); //Если B < A, то меняем их мистами, путём нехитрой
замены
int s = 0;
for (int i = A + 1; i < B; i++) s+= i; //Находим сумму элементов между A и B
for (int i = 0; i < s; i++) cout << s << " "; //Выводим сумму
}
int main()
{
int A, B; //Вводим два числа через пробел
cin >> A >> B;
operation(A, B);
system("pause");
}
15. Вычислить произведение элементов массива, расположенные между первым и
последним отрицательным элементом.
#include <iostream>
using namespace std;
void filling(int const &N, int &ifirst, int &isecond, int *A)
{
for (int i = 0; i < N; i++)
{
cin >> A[i];
if (A[i] < 0 & ifirst == -1)
ifirst = i; //Запоминаем индекс от крайнего слева отрицательного
if (A[i] < 0)
isecond = i; //Запоминаем индекс от крайнего справа отрицательного
}
}
int operation(int &ifirst, int &isecond, int *A)
{
int s = 1;
if (ifirst < isecond) //Если номер первого индекса меньше второго, то считаем
следующим циклом:
for (ifirst++; ifirst < isecond; ifirst++)
s *= A[ifirst]; //Считаем произведение
else //Если номер второго индекса меньше первого, то считаем следующим циклом:
for (isecond++; isecond < ifirst; isecond++)
s *= A[isecond]; //Считаем произведение
return s; //Выводим произведение
}
int main()
{
int N, iplus = -1, isecond = 0;
int A[255] = {0};
cin >> N;
filling(N, iplus, isecond, A);
cout << operation(iplus, isecond, A) << endl;
system("pause");
}
16. Ввести с клавиатуры строку. Определить наибольшее число подряд идущих
пробелов
#include <iostream>
#include <cstring>
using namespace std;
int operation(char *s)
{
int count = 0, max = 0;
for (int i = 0; i < strlen(s); i++)
{
if (s[i] == ' ') count++; //Если элемент строки равен пробелу, то прибавляем к
счётчику единичку
else //Если встретилось слово
{
if (count > max) //Сравниваем количество пробелов перед словом с
максимальным количеством
{
max = count;
count = 0; //Обнуляем счётчик для подсчёта следующих пробелов
}
}
}
return max; //Выводим максимальное количество подряд идущих пробелов
}
int main()
{
char s[250] = {0};
gets(s);
cout << operation(s) << endl;
system("pause");
}
17. Посчитать количество символов в строке между самыми длинным и самым
коротким словом
#include <iostream>
#include <cstring>
using namespace std;
void operation(char *s)
{
int word = 0, min = 255, max = 0, imin, imax, j1, j2, count = 0;
for (int i = 0; i <= strlen(s); i++) //Пробегаем через всю строку (включая
нуль-терминатор)
{
if ((s[i] == '\0') && (word == 0)) //Если встретили нуль-терминатор и проделали все
операции (word = 0), то выходим из цикла
break;
else if ((s[i] != ' ') && (s[i] != '\0')) //Считаем количество букв в слове
word++;
else
{
if (word > max)
{
max = word; //Запоминаем количество букв самого длинного слова
imax = i; //Запоминаем индекс пробела, идущего после последней буквы
этого слова
}
if (word < min)
{
min = word; //Запоминаем количество букв самого короткого слова
imin = i; //Запоминаем индекс пробела, идущего после последней буквы этого
слова
}
word = 0; //Переходим к другому слову, обнуляем количество букв
}
}
if (imax > imin) //Если длинное слова стоит впереди и короткого
{
j2 = (imax - max); //Запоминаем индекс первой буквы длинного слова
j1 = imin; //Запоминаем индекс пробела, идущего после последней буквы
короткого слова
}
else
{
j2 = (imin - min); //Запоминаем индекс первой буквы короткого слова
j1 = imax; //Запоминаем индекс пробела, идущего после последней буквы
длинного слова
}
cout << j2 - j1 << endl; //Считаем количество символом с помощью разности
}
int main()
{
char s[255] = {0};
gets(s);
operation(s);
system("pause");
}
18. Найти наиболее часто встречающиеся число, если их несколько, то наименьшее из
них.
#include <iostream>
using namespace std;
void operation(int &N, int *A)
{
int min = INT_MAX; //Приравниваем минимальное значение к
максимально-возможному
int count1 = 0; //Максимальное количество совпадений
for (int i = 0; i < N; i++) cin >> A[i]; //Считываем массив
for (int i = 0; i < N - 1; i++)
{
int count2 = 0; //Обнуляем количество совпадений
for (int j = i + 1; j < N; j++) //Прогоняем весь массив
if (A[j] == A[i])
count2 += 1; //Если число совпало, то к счётчику прибавляем единичку
if (count2 > count1 || count1 == count2 && A[i] < min) //Если данное количество
больше максимального количества совпадений либо, если количества совпадений
равны, но данное число меньше минимального
{
count1 = count2; //Максимальное количество совпадений равно данному
количеству
min = A[i]; //Минимальное число равно данному числу
}
}
cout << min << endl; //Выводим количество
}
int main()
{
int N;
int *A;
cin >> N;
A = new int [N];
operation(N, A);
system("pause");
}
19. В массиве A, начиная с позиции k, удалить m элементов
#include <iostream>
using namespace std;
void _filling(int k1, int A[])
{
for (int i = 0; i < k1; i++)
{
cout << "[" << i << "]" << ": ";
cin >> A[i];
}
}
void _operation(int k1, int k, int m, int A[])
{
for (int i = 0; i < m; i++) A[k - 1 + i] = 0;
for (int i = 0; i < (k1 - m); i++) A[k - 1 + i] = A[k - 1 + i + m];
}
int main()
{
setlocale(LC_ALL, "rus");
int A[255] = {0};
int k, m, k1;
cout << "Введите размер массива A: ";
cin >> k1;
_filling(k1, A);
cout << "Введите значения k, m: ";
cin >> k >> m;
_operation(k1, k, m, A);
cout << "Массив A:" << endl;
for (int i = 0; i < (k1 - m); i++) cout << A[i] << " ";
system("pause");
}
20. В массиве A, начиная с позиции k, вставить подряд m элементов из массива B,
начинающихся с позиции n.
#include <iostream>
using namespace std;
void _filling(int k1, int m1, int A[], int B[])
{
for (int i = 0; i < k1; i++)
{
cout << "[" << i << "]"
<< ": ";
cin >> A[i];
}
for (int i = 0; i < m1; i++)
{
cout << "[" << i << "]"
<< ": ";
cin >> B[i];
}
}
void _operation(int k1, int m1, int k, int m, int n, int A[], int B[])
{
for (int i = 1; i <= (k1 - k); i++) A[k1 + m - i] = A[k1 - i];
for (int i = 0; i < m; i++) A[k + i] = B[n - 1 + i];
}
int main()
{
setlocale(LC_ALL, "rus");
int A[255] = {0};
int B[255] = {0};
int k, m, n, k1, m1;
cout << "Введите размер массива A: ";
cin >> k1;
cout << "Введите размер массива B: ";
cin >> m1;
_filling(k1, m1, A, B);
cout << "Введите значения k, m, n: ";
cin >> k >> m >> n;
_operation(k1, m1, k, m, n, A, B);
cout << "Массив A:" << endl;
for (int i = 0; i < k1 + m; i++) cout << A[i] << " ";
return 0;
}
21. Убрать все лишние пробелы из строки.
#include <iostream>
#include <cstring>
int main()
{
char s[250];
gets(s);
while (s[0] == ' ')
for (int i = 0; i < strlen(s); i++)
s[i] = s[i + 1];
for (int i = strlen(s); i > 0; --i)
if ((s[i] == ' ') && (s[i - 1] == ' '))
for (int j = i; j < strlen(s); j++)
s[j] = s[j + 1];
puts(s);
}


