
# Методичка по C++

## 1. Введение в C++
**C++** — это мощный язык программирования общего назначения, разработанный Бьярне Страуструпом в 1980-х годах. 
C++ является расширением языка **C** и предоставляет возможности объектно-ориентированного программирования (ООП). 
Он используется для создания высокопроизводительных приложений, игр, драйверов и операционных систем.

### Установка и настройка компилятора
- **g++** (GNU Compiler Collection) можно установить на Linux с помощью команды:
  ```bash
  sudo apt update
  sudo apt install g++
  ```
- **Visual Studio** на Windows поддерживает C++ по умолчанию.
- Онлайн-компиляторы: [Replit](https://replit.com/), [Compiler Explorer](https://godbolt.org/).

---

## 2. Базовые конструкции языка

### Переменные и типы данных
Примеры типов данных в C++:
```cpp
int x = 10;         // Целое число
double pi = 3.14;   // Число с плавающей точкой
char c = 'A';       // Символ
bool flag = true;   // Логический тип
```

### Ввод и вывод (cin, cout)
```cpp
#include <iostream>
using namespace std;

int main() {
    int age;
    cout << "Введите ваш возраст: ";
    cin >> age;
    cout << "Ваш возраст: " << age << endl;
    return 0;
}
```

### Условия (`if`, `else`, `switch`)
```cpp
if (x > 0) {
    cout << "Положительное число";
} else {
    cout << "Отрицательное или ноль";
}
```

---

## 3. Функции
```cpp
int add(int a, int b) {
    return a + b;
}

int main() {
    cout << "Сумма: " << add(5, 3) << endl;
    return 0;
}
```

### Перегрузка функций
```cpp
int multiply(int a, int b) { return a * b; }
double multiply(double a, double b) { return a * b; }
```

---

## 4. Структуры данных
### Массивы
```cpp
int arr[5] = {1, 2, 3, 4, 5};
```

### Векторы
```cpp
#include <vector>
using namespace std;

vector<int> v = {1, 2, 3};
v.push_back(4);
```

### Строки
```cpp
#include <string>
string name = "John";
cout << "Hello, " << name;
```

---

## 5. Работа с памятью
### Указатели
```cpp
int x = 10;
int *ptr = &x;
cout << "Адрес x: " << ptr << ", значение: " << *ptr;
```

### Динамическое выделение памяти
```cpp
int *arr = new int[10];
delete[] arr;
```

---

## 6. Объектно-ориентированное программирование (ООП)
```cpp
class Dog {
public:
    string name;
    void bark() { cout << name << " говорит гав!"; }
};

int main() {
    Dog myDog;
    myDog.name = "Шарик";
    myDog.bark();
    return 0;
}
```

### Наследование
```cpp
class Animal {
public:
    void eat() { cout << "Ем..."; }
};

class Dog : public Animal {
public:
    void bark() { cout << "Гав!"; }
};
```

---

## 7. Шаблоны
### Шаблоны функций
```cpp
template <typename T>
T add(T a, T b) { return a + b; }
```

### Шаблоны классов
```cpp
template <class T>
class Box {
    T value;
public:
    Box(T v) : value(v) {}
    T get() { return value; }
};
```

---

## 8. Работа с файлами
```cpp
#include <fstream>
ofstream file("example.txt");
file << "Hello, file!";
file.close();
```

---

## 9. Современные возможности C++ (C++11 и выше)
### Лямбда-функции
```cpp
auto sum = [](int a, int b) { return a + b; };
cout << sum(3, 4);
```

### `std::thread` и многопоточность
```cpp
#include <thread>
void hello() { cout << "Привет из потока!"; }

int main() {
    thread t(hello);
    t.join();
    return 0;
}
```

---

## 10. Полезные советы и примеры
- **Отладка**: используйте `gdb` или встроенные инструменты в IDE.
- **Типичные ошибки**: неопределённое поведение при выходе за пределы массива, утечки памяти при использовании `new` без `delete`.

---

**Автор**: Методичка по C++ для начинающих.
