# cpp-mython
Учебный проект Яндекс.Практикума. Интерпретатор языка Mython.

Реализация на с++ интерпретатора языка программирования Mython — упрощённое подмножество Python.
Язык является динамически типизированным, поддерживает классы и наследование. Все методы в классах по умолчанию виртуальные.
## Сборка проекта
Для сборки программы необходим компилятор С++ поддерживающий стандарт не ниже С++17 и установленная утилита CMake.
## Использование интерпретатора
На вход поступает текст программы, а интерпретатор должен вывести в выходной поток результат всех команд print.
Примеры вызовов в main.cpp 

## Описание языка Mython
### **Числа**
В языке Mython используются только целые числа. С ними можно выполнять обычные арифметические операции: сложение, вычитание, умножение, целочисленное деление.

### **Строки**
Строковая константа в Mython — это последовательность произвольных символов, размещающаяся на одной строке и ограниченная двойными кавычками `"` или одинарными `'`. Поддерживается экранирование спецсимволов `'\n'`, `'\t'`, `'\''` и `'\"'`. Примеры строк в Mython:
 - `"hello"`
 - `'world'`
 - `'long string with a double quote " inside'`
 - `"another long string with a single quote ' inside"`
 - `"string with a double quote \" inside"`
 - `'string with a single quote \' inside'`
 - `''`, `""` — пустые строки.
Строки в Mython — неизменяемые.

### **Логические константы и None**
Кроме строковых и целочисленных значений язык Mython поддерживает логические значения `True` и `False`. Есть также специальное значение `None`, аналог `nullptr` в С++. В отличие от C++, логические константы пишутся с большой буквы.

### **Комментарии**
Mython поддерживает однострочные комментарии, начинающиеся с символа `#`. Весь следующий текст до конца текущей строки игнорируется. `#` внутри строк считается обычным символом.

```python
# это комментарий
x = 5 #это тоже комментарий
# в следующей строке # - обычный символ
hashtag = "#природа"
```

### **Идентификаторы**
Идентификаторы в Mython используются для обозначения имён переменных, классов и методов. Об этом далее. Идентификаторы формируются так же, как в большинстве других языков программирования: начинаются со строчной или заглавной латинской буквы либо с символа подчёркивания. Потом следует произвольная последовательность, состоящая из цифр, букв и символа подчёркивания.

Примеры правильных идентификаторов: `x`, `_42`, `do_something`, `int2str`. Примеры неправильных идентификаторов:
 - `4four` — начинается с цифры;
 - `one;two` — содержит символ, который не относится к цифрам, буквам или знакам подчёркивания.

### **Классы**
Объявление класса начинается с ключевого слова `class`, за которым следует идентификатор имени и объявление методов класса. Пример класса «Прямоугольник»:

```python
class Rect:
  def __init__(w, h):
    self.w = w
    self.h = h

  def area():
    return self.w * self.h
```
Специальный метод `__init__` играет роль конструктора — он автоматически вызывается при создании нового объекта класса. Метод `__init__` может отсутствовать.

Неявный параметр всех методов — специальный параметр `self`, аналог указателя `this` в C++. Параметр `self` ссылается на текущий объект класса.

Поля не объявляются заранее, а добавляются в объект класса при первом присваивании. Поэтому обращения к полям класса всегда надо начинать с `self.`, чтобы отличать их от локальных переменных.

Все поля объекта — публичные.

```python
r = Rect(10, 5)
```
В этой программе создаётся новый объект класса `Rect`. При вызове метода `__init__` параметр `w` будет иметь значение 10, а параметр `h` — 5. Созданный прямоугольник будет доступен в переменной `r`.

### **Типизация**
Mython — это язык с динамической типизацией. В нём тип каждой переменной определяется во время исполнения программы и может меняться в ходе её работы. Поэтому вместо «присваивания переменной значения» лучше говорить о «связывании значения с некоторым именем». Благодаря динамической типизации при первом использовании переменной не надо указывать её тип. Пример:

```python
x = 4  # переменная x связывается с целочисленным значением 4
# следующей командой переменная x связывается со значением 'hello'
x = 'hello'
y = True
x = y
```

### **Операции**
В Mython определены:
 - Арифметические операции для целых чисел, деление выполняется нацело. Деление на ноль вызывает ошибку времени выполнения.
 - Операция конкатенации строк, например: `s = 'hello, ' + 'world'`.
 - Операции сравнения строк и целых чисел `==`, `!=`, `<=`, `>=`, `<`, `>`; сравнение строк выполняется лексикографически.
 - Логические операции `and`, `or`, `not`.
 - Унарный минус.

Приоритет операций (в порядке убывания приоритета):
 - Унарный минус.
 - Умножение и деление.
 - Сложение и вычитание.
 - Операции сравнения.
 - Логические операции.

Порядок вычисления выражений может быть изменён скобками:
```python
print 2 + 3 * 4   # выведет 14
print (2 + 3) * 4 # выведет 20
```

В Mython операция сложения кроме чисел и строк применима к объектам классов со специальным методом `__add__`:
```python
class Fire:
  def __init__(obj):
    self.obj = obj

  def __str__():
    return "Burnt " + str(self.obj)

class Tree:
  def __str__():
    return "tree"

class Matches: # Спички
  # операция сложения спичек с другими объектами превращает их в огонь
  def __add__(smth):
    return Fire(smth)

result = Matches() + Tree()
print result             # Выведет Burnt tree
print Matches() + result # Выведет Burnt Burnt tree
```

Операции сравнения применяются не только к числам и строкам, но и к объектам классов, имеющих методы `__eq__` (проверка «равно») и `__lt__` (проверка «меньше»). Используя эти методы, можно реализовать все операции сравнения.
```python
class Person:
  def __init__(name, age):
    self.name = name
    self.age = age
  def __eq__(rhs):
    return self.name == rhs.name and self.age == rhs.age
  def __lt__(rhs):
    if self.name < rhs.name:
        return True
    return self.name == rhs.name and self.age < rhs.age

print Person("Ivan", 10) <= Person("Sergey", 10) # True
print Person("Ivan", 10) <= Person("Sergey", 9)  # False
```

### **Функция str**
Функция `str` преобразует переданный ей аргумент в строку. Если аргумент — объект класса, она вызывает у него специальный метод `__str__` и возвращает результат. Если метода `__str__` в классе нет, функция возвращает строковое представление адреса объекта в памяти. Примеры:
 - `str('Hello')` вернёт строку `Hello`;
 - `str(100500)` вернёт строку `100500`;
 - `str(False)` вернёт строку `False`;
 - `str(Rect(3, 4))` вернёт адрес объекта в памяти, например `0x2056fd0`.

Пример класса с методом `__str__`:
```python
class Rect(Shape):
  def __init__(w, h):
    self.w = w
    self.h = h

  def __str__():
    return "Rect(" + str(self.w) + 'x' + str(self.h) + ')'
```
Выражение `str(Rect(3, 4))` вернёт строку `Rect(3x4)`.

### **Команда print**
Специальная команда `print` принимает набор аргументов, разделённых запятой, печатает их в стандартный вывод и дополнительно выводит перевод строки. Посмотрите на этот код:
```python
x = 4
w = 'world'
print x, x + 6, 'Hello, ' + w
```
Он выведет:
`4 10 Hello, world `

Команда `print` вставляет пробел между выводимыми значениями. Если ей не передать аргументы, она просто выведет перевод строки.

Чтобы преобразовать каждый свой аргумент в строку, команда `print` вызывает для него функцию `str`. Таким образом, команда `print Rect(20, 15)` выведет в `stdout` строку `Rect(20x15)`.

### **Условный оператор**
В Mython есть условный оператор. Его синтаксис:
```python
if <условие>:
  <действие 1>
  <действие 2>
  ...
  <действие N>
else:
  <действие 1>
  <действие 2>
  ...
  <действие M>
```

`<условие>` — это произвольное выражение, за которым следует двоеточие. Если условие истинно, выполняются действия под веткой `if`, если ложно — действия под веткой `else`. Наличие ветки `else` необязательно.

`<условие>` может содержать сравнения, а также логические операции `and`, `or` и `not`. Условие будет истинным или ложным в зависимости от того, какой тип имеет вычисленное выражение.

Если результат вычисления условия — значение логического типа, для проверки истинности условия используется именно оно. Примеры:
 - `if x > 0:`
 - `if s != 'Jack' and s != 'Ann':`

Если результат вычисления условия — число, условие истинно тогда и только тогда, когда это число не равно нулю, как в C/C++, например, `if x + y:`.

Если результат вычисления условия — строка, условие истинно тогда и только тогда, когда эта строка имеет ненулевую длину.

Если результат вычисления условия — объект класса, условие истинно.

Если результат вычисления условия — `None`, условие ложно.

Действия в ветках `if` и `else` набраны с отступом в два пробела. В языке Mython команды объединяются в блоки отступами. Один отступ равен двум пробелам. Отступ в нечётное количество пробелов считается некорректным.

### **Наследование**
В языке Mython у класса может быть один родительский класс. Если он есть, он указывается в скобках после имени класса и до символа двоеточия. В примере ниже класс `Rect` наследуется от класса `Shape`:

```python
class Shape:
  def __str__():
    return "Shape"

  def area():
    return 'Not implemented'

class Rect(Shape):
  def __init__(w, h):
    self.w = w
    self.h = h

  def __str__():
    return "Rect(" + str(self.w) + 'x' + str(self.h) + ')'

  def area():
    return self.w * self.h
```

Наследование в Mython работает так же, как в Python, — все методы родительского класса становятся доступны классу-потомку. При этом все методы публичные и виртуальные. Например, код ниже выведет `Hello, John`:
```python
class Greeting:
  def greet():
    return "Hello, " + self.name()

  def name():
    return 'Noname'

class HelloJohn(Greeting):
  def name():
    return 'John'

greet_john = HelloJohn()
print greet_john.greet()
```

### **Методы**
Методы в Mython имеют синтаксис:
```python
def <имя метода>(<список параметров>):
  <действие 1>
  <действие 2>
  ...
  <действие N>
```

Ключевое слово `def` располагается с отступом в два пробела относительно класса. Инструкции, составляющие тело метода, имеют отступ в два пробела относительно ключевого слова `def`.

Как и в случае полей класса, обращения к полям и методам текущего класса надо начинать с `self.`:
```python
class Factorial:
  def calc(n):
    if n == 0:
      return 1
    return n * self.calc(n - 1)

fact = Factorial()
print fact.calc(4) # Prints 24
```

Этот пример также показывает поддержку рекурсии, которая компенсирует отсутствие циклов в языке.

Команда `return` завершает выполнение метода и возвращает из него результат вычисления своего аргумента. Если исполнение метода не достигает команды `return`, метод возвращает `None`.

### **Семантика присваивания**
Как сказано выше, Mython — это язык с динамической типизацией, поэтому операция присваивания имеет семантику не копирования значения в область памяти, а связывания имени переменной со значением. Как следствие, переменные только ссылаются на значения, а не содержат их копии. Говоря терминологией С++, переменные в Mython — указатели. Аналог `nullptr` — значение `None`. Код ниже выведет `2`, так как переменные `x` и `y` ссылаются на один и тот же объект:
```python
class Counter:
  def __init__():
    self.value = 0

  def add():
    self.value = self.value + 1

x = Counter()
y = x
x.add()
y.add()
print x.value
```

### **Прочие ограничения**
Результат вызова метода или конструктора в Mython — терминальная операция. Её результат можно присвоить переменной или использовать в виде параметра функции или команды, но обратиться к полям и методам возвращённого объекта напрямую нельзя:
```python
# Так нельзя
print Rect(10, 5).w
# А вот так можно
r = Rect(10, 5)
print r.w
```
