# Решения Level 2 (Advanced)

**Уровень**: Продвинутый (знаете функции, списки, словари, условия)

---

## 📚 Оглавление

1. [PRIMM - Решения](#primm-решения)
2. [Parson Problems - Решения](#parson-problems-решения)
3. [TDD - Решения](#tdd-решения)
4. [Справочник синтаксиса](#справочник-синтаксиса)
5. [Ответы на вопросы](#ответы-на-вопросы)

---

## PRIMM - Решения

### Задание 1: greet()

```python
def greet(name):
    return f"Привет, {name}!"

print(greet("Алиса"))  # Привет, Алиса!
```

---

### Задание 2: create_email()

```python
def create_email(name, domain):
    return f"{name}@{domain}"

print(create_email("alice", "example.com"))  # alice@example.com
```

---

### Творческое задание 1: Конвертер температуры

```python
def celsius_to_fahrenheit(c):
    return c * 9/5 + 32

def fahrenheit_to_celsius(f):
    return (f - 32) * 5/9

# Проверка
print(celsius_to_fahrenheit(0))    # 32.0
print(celsius_to_fahrenheit(100))  # 212.0
print(fahrenheit_to_celsius(32))   # 0.0
```

---

### Задание 3: Телефонная книга

```python
contacts = {
    "Алиса": "123-45-67",
    "Боб": "234-56-78",
    "Ева": "345-67-89"
}

# 1. Номер Алисы
print(contacts["Алиса"])  # 123-45-67

# 2. Добавить Еву (уже есть, но можно добавить ещё)
contacts["Карл"] = "456-78-90"

# 3. Изменить номер Боба
contacts["Боб"] = "999-99-99"

# 4. Вывести весь словарь
print(contacts)
```

---

### Задание 4: Подсчёт частоты слов

```python
words = ["яблоко", "банан", "яблоко", "апельсин", "банан", "яблоко"]

count = {}
for word in words:
    if word in count:
        count[word] += 1
    else:
        count[word] = 1

print(count)
# {'яблоко': 3, 'банан': 2, 'апельсин': 1}
```

**Продвинутый вариант (Counter)**:
```python
from collections import Counter

words = ["яблоко", "банан", "яблоко", "апельсин", "банан", "яблоко"]
count = dict(Counter(words))
print(count)
```

---

### Задание 5: Факториал (рекурсия)

```python
def factorial(n):
    if n <= 1:
        return 1
    return n * factorial(n - 1)

print(factorial(5))  # 120
print(factorial(3))  # 6
print(factorial(1))  # 1
print(factorial(0))  # 1
```

**Как это работает**:
```
factorial(5)
= 5 * factorial(4)
= 5 * (4 * factorial(3))
= 5 * (4 * (3 * factorial(2)))
= 5 * (4 * (3 * (2 * factorial(1))))
= 5 * (4 * (3 * (2 * 1)))
= 120
```

---

### Задание 6: Сумма цифр числа (рекурсия)

```python
def sum_digits(n):
    if n < 10:
        return n
    return (n % 10) + sum_digits(n // 10)

print(sum_digits(123))  # 6 (1+2+3)
print(sum_digits(5))    # 5
print(sum_digits(999))  # 27 (9+9+9)
```

**Как это работает**:
```
sum_digits(123)
= (123 % 10) + sum_digits(123 // 10)
= 3 + sum_digits(12)
= 3 + (12 % 10) + sum_digits(12 // 10)
= 3 + 2 + sum_digits(1)
= 3 + 2 + 1
= 6
```

---

### Задание 7: Анализатор студентов

```python
def analyze_students(students):
    average = sum(students.values()) / len(students)
    best_student = max(students, key=students.get)
    worst_student = min(students, key=students.get)

    return {
        "средний_балл": int(average),
        "лучший_студент": best_student,
        "худший_студент": worst_student
    }

students = {"Алиса": 85, "Боб": 92, "Ева": 78}
print(analyze_students(students))
```

**Альтернативный вариант (через цикл)**:
```python
def analyze_students(students):
    total = 0
    best_name = ""
    best_score = -1
    worst_name = ""
    worst_score = 101

    for name, score in students.items():
        total += score
        if score > best_score:
            best_score = score
            best_name = name
        if score < worst_score:
            worst_score = score
            worst_name = name

    return {
        "средний_балл": total // len(students),
        "лучший_студент": best_name,
        "худший_студент": worst_name
    }
```

---

### Итоговое задание: Библиотека книг

```python
books = {
    "1984": {"автор": "Оруэлл", "год": 1949, "прочитана": True},
    "Война и мир": {"автор": "Толстой", "год": 1869, "прочитана": False},
    "Мастер и Маргарита": {"автор": "Булгаков", "год": 1967, "прочитана": False}
}

def add_book(books, title, author, year, read):
    books[title] = {
        "автор": author,
        "год": year,
        "прочитана": read
    }

def mark_as_read(books, title):
    if title in books:
        books[title]["прочитана"] = True

def get_unread_books(books):
    unread = []
    for title, info in books.items():
        if not info["прочитана"]:
            unread.append(title)
    return unread

def get_statistics(books):
    total = len(books)
    read_count = 0

    for title, info in books.items():
        if info["прочитана"]:
            read_count += 1

    return {
        "всего_книг": total,
        "прочитано": read_count,
        "не_прочитано": total - read_count
    }

# Тестирование
add_book(books, "Преступление и наказание", "Достоевский", 1866, False)
mark_as_read(books, "Война и мир")
print("Непрочитанные:", get_unread_books(books))
print("Статистика:", get_statistics(books))
```

**Продвинутый вариант (list comprehension)**:
```python
def get_unread_books(books):
    return [title for title, info in books.items() if not info["прочитана"]]
```

---

## Parson Problems - Решения

### Задача 1: Функция факториала

**Правильный порядок** (вариант 1):
```python
def factorial(n):
    if n <= 1:
        return 1
    return n * factorial(n - 1)

print(factorial(5))
```

**Правильный порядок** (вариант 2 с else):
```python
def factorial(n):
    if n <= 1:
        return 1
    else:
        return n * factorial(n - 1)

print(factorial(5))
```

**Что было лишним**:
- `B) def factorial(n, result):` — не нужен второй параметр
- `E) return n` — базовый случай должен возвращать 1
- `H) return n + factorial(n - 1)` — умножение, а не сложение!

---

### Задача 2: Поиск в словаре

**Правильный порядок**:
```python
students = {"Алиса": 85, "Боб": 92, "Ева": 78}
max_score = 0  # или -1 (лучше для отрицательных баллов)
best_student = ""
for name, score in students.items():
    if score > max_score:
        max_score = score
        best_student = name
print(f"Лучший студент: {best_student} с баллом {max_score}")
```

**Что было лишним**:
- `F) for name in students:` — нет переменной score

---

### Задача 3: Функция Фибоначчи

**Правильный порядок** (вариант 1 — длинный):
```python
def fibonacci(n):
    if n <= 0:
        return 0
    elif n == 1:
        return 1
    return fibonacci(n - 1) + fibonacci(n - 2)

print(fibonacci(0))
print(fibonacci(1))
print(fibonacci(5))
print(fibonacci(7))
```

**Правильный порядок** (вариант 2 — короткий):
```python
def fibonacci(n):
    if n < 2:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)

print(fibonacci(0))
print(fibonacci(1))
print(fibonacci(5))
print(fibonacci(7))
```

**Что было лишним**:
- `H) return n * fibonacci(n - 1)` — сложение, не умножение!
- `F) else:` — опционально

---

### Задача 4: Создание словаря из списков

**Правильный порядок** (вариант 1 — через индексы):
```python
keys = ["имя", "возраст", "город"]
values = ["Алиса", 15, "Москва"]
result = {}
for i in range(len(keys)):
    result[keys[i]] = values[i]
print(result)
```

**Правильный порядок** (вариант 2 — через zip):
```python
keys = ["имя", "возраст", "город"]
values = ["Алиса", 15, "Москва"]
result = {}
for key, value in zip(keys, values):
    result[key] = value
print(result)
```

**Что было лишним**:
- `D) result = []` — нужен словарь, не список!
- `I) result.append((keys[i], values[i]))` — append для списков

---

### Задача 5: Инвертирование словаря

**Правильный порядок**:
```python
def invert_dict(d):
    result = {}
    for key, value in d.items():
        result[value] = key
    return result

original = {"a": 1, "b": 2, "c": 3}
inverted = invert_dict(original)
print(inverted)
```

**Что было лишним**:
- `C) result = []` — словарь, не список
- `E) for key in d:` — нужны и key, и value
- `G) result[key] = value` — неправильно! Должно быть result[value] = key

---

### Задача 6: Рекурсивный поиск суммы

**Правильный порядок** (вариант 1):
```python
def sum_list(numbers):
    if len(numbers) == 0:
        return 0
    return numbers[0] + sum_list(numbers[1:])

print(sum_list([1, 2, 3, 4, 5]))
```

**Правильный порядок** (вариант 2):
```python
def sum_list(numbers):
    if numbers == []:
        return 0
    return numbers[0] + sum_list(numbers[1:])

print(sum_list([1, 2, 3, 4, 5]))
```

**Что было лишним**:
- `G) return numbers[0] + sum_list(numbers[:-1])` — numbers[:-1] это все кроме последнего, нужно [1:]!
- `E) else:` — опционально

---

### Задача 7: Фильтрация словаря

**Правильный порядок** (вариант 1 — цикл):
```python
students = {"Алиса": 85, "Боб": 75, "Ева": 90, "Дима": 70}
result = {}
for name, score in students.items():
    if score >= 80:
        result[name] = score
print(result)
```

**Правильный порядок** (вариант 2 — dict comprehension):
```python
students = {"Алиса": 85, "Боб": 75, "Ева": 90, "Дима": 70}
result = {name: score for name, score in students.items() if score >= 80}
print(result)
```

**Что было лишним**:
- `D) for name in students.keys():` — нет переменной score

---

### Бонус: Группировка по первой букве

**Правильный порядок**:
```python
words = ["apple", "apricot", "banana", "blueberry", "cherry"]
result = {}
for word in words:
    first_letter = word[0]
    if first_letter not in result:
        result[first_letter] = []
    result[first_letter].append(word)
print(result)
```

**Что было лишним**:
- `E) first_letter = word[1]` — вторая буква, не первая!
- `H) result[first_letter] = {}` — список, не словарь!
- `J) result[first_letter] = word` — заменит, а не добавит!

---

## TDD - Решения

### Задача 1: Шифр Цезаря

```python
def caesar_cipher(text, shift):
    result = ""
    for char in text:
        if char.isalpha():
            # Определяем базу (A или a)
            base = ord('A') if char.isupper() else ord('a')
            # Сдвигаем букву
            shifted = (ord(char) - base + shift) % 26 + base
            result += chr(shifted)
        else:
            # Не буква — оставляем как есть
            result += char
    return result
```

---

### Задача 2: Решето Эратосфена

```python
def sieve_of_eratosthenes(n):
    if n < 2:
        return []

    # Создаём список от 2 до n
    is_prime = [True] * (n + 1)
    is_prime[0] = is_prime[1] = False

    for i in range(2, int(n**0.5) + 1):
        if is_prime[i]:
            # Отмечаем все кратные i как составные
            for j in range(i*i, n + 1, i):
                is_prime[j] = False

    # Собираем все простые
    primes = [i for i in range(2, n + 1) if is_prime[i]]
    return primes
```

---

### Задача 3: Проверка анаграммы

```python
def is_anagram(str1, str2):
    # Убираем пробелы и приводим к нижнему регистру
    s1 = str1.replace(" ", "").lower()
    s2 = str2.replace(" ", "").lower()

    # Сортируем и сравниваем
    return sorted(s1) == sorted(s2)
```

**Альтернатива (через Counter)**:
```python
from collections import Counter

def is_anagram(str1, str2):
    s1 = str1.replace(" ", "").lower()
    s2 = str2.replace(" ", "").lower()
    return Counter(s1) == Counter(s2)
```

---

### Задача 4: Обратная польская запись (RPN)

```python
def evaluate_rpn(tokens):
    stack = []

    for token in tokens:
        if token in ['+', '-', '*', '/']:
            # Оператор — достать два числа
            b = stack.pop()
            a = stack.pop()

            if token == '+':
                result = a + b
            elif token == '-':
                result = a - b
            elif token == '*':
                result = a * b
            elif token == '/':
                result = int(a / b)  # Деление с округлением к нулю

            stack.append(result)
        else:
            # Число — положить в стек
            stack.append(int(token))

    return stack[0]
```

---

### Задача 5: Группировка анаграмм

```python
def group_anagrams(words):
    from collections import defaultdict

    groups = defaultdict(list)

    for word in words:
        # Сортированное слово как ключ
        key = ''.join(sorted(word.lower()))
        groups[key].append(word)

    return list(groups.values())
```

**Альтернатива (без defaultdict)**:
```python
def group_anagrams(words):
    groups = {}

    for word in words:
        key = ''.join(sorted(word.lower()))
        if key not in groups:
            groups[key] = []
        groups[key].append(word)

    return list(groups.values())
```

---

### Задача 6: LRU Cache

```python
class LRUCache:
    def __init__(self, capacity):
        self.capacity = capacity
        self.cache = {}  # {ключ: значение}
        self.order = []  # Порядок использования (новые в конце)

    def get(self, key):
        if key not in self.cache:
            return -1

        # Обновляем порядок (перемещаем в конец)
        self.order.remove(key)
        self.order.append(key)
        return self.cache[key]

    def put(self, key, value):
        if key in self.cache:
            # Ключ уже есть — обновляем значение и порядок
            self.order.remove(key)
        elif len(self.cache) >= self.capacity:
            # Кэш полон — удаляем самый старый
            oldest = self.order.pop(0)
            del self.cache[oldest]

        # Добавляем новый элемент
        self.cache[key] = value
        self.order.append(key)
```

---

### Задача 7: Поиск в глубину (DFS)

```python
def dfs(graph, start):
    visited = []
    stack = [start]

    while stack:
        node = stack.pop()
        if node not in visited:
            visited.append(node)
            # Добавляем соседей в стек
            for neighbor in reversed(graph.get(node, [])):
                if neighbor not in visited:
                    stack.append(neighbor)

    return visited
```

**Рекурсивная версия**:
```python
def dfs(graph, start, visited=None):
    if visited is None:
        visited = []

    visited.append(start)

    for neighbor in graph.get(start, []):
        if neighbor not in visited:
            dfs(graph, neighbor, visited)

    return visited
```

---

### Задача 8: Поиск в ширину (BFS)

```python
def bfs(graph, start):
    from collections import deque

    visited = []
    queue = deque([start])

    while queue:
        node = queue.popleft()
        if node not in visited:
            visited.append(node)
            # Добавляем соседей в очередь
            for neighbor in graph.get(node, []):
                if neighbor not in visited:
                    queue.append(neighbor)

    return visited
```

---

## Справочник синтаксиса

### Функции

```python
# Определение функции
def имя_функции(параметр1, параметр2):
    # код
    return результат

# Вызов
результат = имя_функции(значение1, значение2)

# Без return — возвращает None
def print_hello():
    print("Hello")
    # return None (неявно)

# Возврат нескольких значений
def min_max(numbers):
    return min(numbers), max(numbers)

minimum, maximum = min_max([1, 2, 3, 4, 5])
```

---

### Словари (dict)

```python
# Создание
person = {
    "имя": "Алиса",
    "возраст": 15
}

# Доступ
print(person["имя"])  # "Алиса"

# Добавление/изменение
person["город"] = "Москва"
person["возраст"] = 16

# Проверка наличия ключа
if "имя" in person:
    print("Ключ есть!")

# Методы
person.keys()      # dict_keys(['имя', 'возраст', 'город'])
person.values()    # dict_values(['Алиса', 16, 'Москва'])
person.items()     # dict_items([('имя', 'Алиса'), ...])

# Перебор
for key, value in person.items():
    print(f"{key}: {value}")

# Удаление
del person["город"]
value = person.pop("возраст")  # Вернёт 16 и удалит

# Значение по умолчанию
age = person.get("возраст", 0)  # Вернёт 0, если ключа нет

# Dict comprehension
squares = {x: x**2 for x in range(5)}
# {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```

---

### Рекурсия

```python
# Структура рекурсивной функции
def рекурсивная_функция(параметр):
    # Базовый случай (условие остановки)
    if условие_остановки:
        return базовое_значение

    # Рекурсивный случай
    return рекурсивная_функция(измененный_параметр)

# Примеры
def countdown(n):
    if n <= 0:           # Базовый случай
        print("Пуск!")
    else:                # Рекурсивный случай
        print(n)
        countdown(n - 1)

def factorial(n):
    if n <= 1:
        return 1
    return n * factorial(n - 1)

def fibonacci(n):
    if n < 2:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)
```

**⚠️ Важно**:
- Всегда должен быть базовый случай (иначе бесконечная рекурсия!)
- Параметр ОБЯЗАТЕЛЬНО должен изменяться и приближаться к базовому случаю

---

### Продвинутые техники

#### List Comprehension
```python
# Базовый
squares = [x**2 for x in range(10)]

# С условием
evens = [x for x in range(10) if x % 2 == 0]

# С функцией
words = ["hello", "world"]
upper = [w.upper() for w in words]
```

#### Dict Comprehension
```python
# Базовый
squares = {x: x**2 for x in range(5)}

# С условием
high_scores = {name: score for name, score in students.items() if score >= 80}
```

#### Set Comprehension
```python
unique_lengths = {len(word) for word in words}
```

#### Генераторы
```python
# Ленивое вычисление (не создаёт список сразу)
gen = (x**2 for x in range(1000000))

# Использование
for value in gen:
    print(value)
```

#### Lambda функции
```python
# Анонимная функция
add = lambda x, y: x + y
print(add(3, 5))  # 8

# С map/filter
numbers = [1, 2, 3, 4, 5]
squared = list(map(lambda x: x**2, numbers))
evens = list(filter(lambda x: x % 2 == 0, numbers))

# Как ключ сортировки
students = {"Боб": 92, "Алиса": 85}
best = max(students, key=lambda name: students[name])
```

#### Collections
```python
from collections import Counter, defaultdict, deque

# Counter — подсчёт элементов
words = ["apple", "banana", "apple"]
counts = Counter(words)  # Counter({'apple': 2, 'banana': 1})

# defaultdict — словарь с значением по умолчанию
groups = defaultdict(list)
groups["a"].append("apple")  # Не нужна проверка if "a" in groups

# deque — двусторонняя очередь (быстрые операции с краёв)
queue = deque([1, 2, 3])
queue.append(4)       # [1, 2, 3, 4]
queue.appendleft(0)   # [0, 1, 2, 3, 4]
queue.pop()           # 4, остаётся [0, 1, 2, 3]
queue.popleft()       # 0, остаётся [1, 2, 3]
```

---

## Ответы на вопросы

### 1. Что возвращает функция без return?

**Ответ**: `None` (специальное значение "ничего")

```python
def no_return():
    print("Hello")

result = no_return()  # Выведет "Hello"
print(result)         # None
```

---

### 2. В чём разница между параметрами и аргументами?

**Ответ**:
- **Параметры** — переменные в определении функции
- **Аргументы** — значения при вызове функции

```python
def greet(name):  # name — параметр
    print(f"Привет, {name}!")

greet("Алиса")    # "Алиса" — аргумент
```

---

### 3. Как добавить элемент в словарь?

**Ответ**: `словарь[ключ] = значение`

```python
person = {}
person["имя"] = "Алиса"      # Добавление
person["возраст"] = 15       # Добавление
person["возраст"] = 16       # Изменение (ключ уже есть)
```

---

### 4. Что такое базовый случай в рекурсии?

**Ответ**: Условие остановки рекурсии. Случай, когда функция НЕ вызывает сама себя, а возвращает результат напрямую.

```python
def factorial(n):
    if n <= 1:        # ← Базовый случай (СТОП!)
        return 1
    return n * factorial(n - 1)  # Рекурсивный случай
```

Без базового случая → бесконечная рекурсия → ошибка!

---

### 5. Почему важно изменять параметр в рекурсии?

**Ответ**: Чтобы рано или поздно достичь базового случая и остановиться.

```python
# ✅ Правильно — параметр уменьшается
def countdown(n):
    if n <= 0:
        return
    print(n)
    countdown(n - 1)  # n уменьшается → дойдём до 0

# ❌ НЕПРАВИЛЬНО — бесконечная рекурсия!
def bad_countdown(n):
    if n <= 0:
        return
    print(n)
    bad_countdown(n)  # n НЕ изменяется → никогда не дойдём до 0!
```

---

### 6. Как получить все ключи словаря?

**Ответ**: `словарь.keys()`

```python
person = {"имя": "Алиса", "возраст": 15}

keys = person.keys()           # dict_keys(['имя', 'возраст'])
keys_list = list(person.keys())  # ['имя', 'возраст']

# Перебор
for key in person.keys():
    print(key)
```

---

### 7. Что быстрее: поиск в списке или в словаре? Почему?

**Ответ**: **Словарь намного быстрее!**

- **Список**: O(n) — нужно проверить каждый элемент
- **Словарь**: O(1) — мгновенный доступ по хэш-таблице

```python
# Список — медленно для больших данных
my_list = [1, 2, 3, ..., 1000000]
if 999999 in my_list:  # Проверит ~миллион элементов!
    print("Найдено")

# Словарь — мгновенно
my_dict = {i: True for i in range(1000000)}
if 999999 in my_dict:  # Мгновенная проверка!
    print("Найдено")
```

---

### 8. Когда использовать рекурсию, а когда цикл?

**Рекурсия подходит для**:
- Задач с естественной рекурсивной структурой (дерево, факториал, Фибоначчи)
- Когда нужен элегантный короткий код
- Задачи типа "разделяй и властвуй"

**Цикл подходит для**:
- Простых повторений
- Когда важна производительность (рекурсия медленнее!)
- Итерация по коллекциям

**Пример — Фибоначчи**:

Рекурсия (элегантно, но медленно):
```python
def fib(n):
    if n < 2:
        return n
    return fib(n-1) + fib(n-2)
```

Цикл (быстрее):
```python
def fib(n):
    if n < 2:
        return n
    a, b = 0, 1
    for _ in range(2, n + 1):
        a, b = b, a + b
    return b
```

**Правило**: Если можно легко написать циклом — используйте цикл!

---

## 🎯 Следующие шаги

После Level 2 вы готовы к:

1. **Олимпиадные задачи** — LeetCode, Codeforces, HackerRank
2. **Структуры данных** — стеки, очереди, деревья, графы
3. **Алгоритмы** — сортировка, поиск, динамическое программирование
4. **ООП** — классы, наследование, полиморфизм
5. **Работа с библиотеками** — NumPy, Pandas, Matplotlib

---

## 💡 Дополнительные ресурсы

### Практика:
- [LeetCode](https://leetcode.com/) — олимпиадные задачи
- [Codeforces](https://codeforces.com/) — соревнования по программированию
- [HackerRank](https://www.hackerrank.com/) — задачи с автопроверкой

### Алгоритмы:
- [VisuAlgo](https://visualgo.net/en) — визуализация алгоритмов
- [Algorithm Visualizer](https://algorithm-visualizer.org/) — интерактивные алгоритмы

### Книги:
- "Грокаем алгоритмы" — Адитья Бхаргава
- "Совершенный код" — Стив Макконнелл

---

**Поздравляем с прохождением Level 2!** 🎉🏆

Вы научились работать с функциями, словарями, рекурсией и решать сложные алгоритмические задачи. Теперь готовы к олимпиадам и серьёзным проектам!
