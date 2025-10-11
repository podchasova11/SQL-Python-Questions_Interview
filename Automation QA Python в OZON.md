Это поисковый запрос для HeadHunter, чтобы найти релевантные, вакансии на Python AQA, ищем вакансии и требования в них https://hh.ru/search/vacancy?text=Name%3A%28python+or+qa+automation++or+AQA%29+and+DESCRIPTION%3A%28python+or+qa+automation%29+NOT+middle+NOT+%D0%BC%D0%B5%D0%BD%D1%82%D0%BE%D1%80+NOT+Senior+not+%D0%9F%D1%80%D0%B5%D0%BF%D0%BE%D0%B4%D0%B0%D0%B2%D0%B0%D1%82%D0%B5%D0%BB%D1%8C+NOT+TechLead+NOT+%D1%82%D0%B5%D1%85%D0%BB%D0%B8%D0%B4+NOT+middle%2B&salary=&no_magic=true&ored_clusters=true&items_on_page=100&search_field=name&excluded_text=&hhtmFrom=vacancy_search_list&hhtmFromLabel=vacancy_search_line

### Технические вопросы по Python:
1. **Что такое GIL в Python и как он влияет на многопоточность?**
   - **Global Interpreter Lock (GIL)** — это механизм в CPython, который обеспечивает выполнение только одного потока в любой момент времени. Это ограничивает многопоточность на уровне интерпретатора, но не мешает многопроцессным приложениям. GIL может снижать производительность в CPU-интенсивных многопоточных задачах, но не влияет на I/O-интенсивные задачи.

2. **Чем отличаются списки (list) и кортежи (tuple) в Python?**
   - **Списки** изменяемы (могут изменяться после создания), поддерживают множество методов для изменения своих элементов.
   - **Кортежи** неизменяемы (после создания их содержимое нельзя изменить), имеют фиксированную структуру и обычно занимают меньше памяти, чем списки.

3. **Объясните разницу между глубоким и поверхностным копированием (deep copy и shallow copy).**
   - **Поверхностное копирование (shallow copy)** создает новый объект, но вложенные объекты внутри него остаются ссылками на оригинальные объекты.
     ```python
     import copy
     original = [[1, 2, 3], [4, 5, 6]]
     shallow_copy = copy.copy(original)
     ```
   - **Глубокое копирование (deep copy)** создает новый объект, а также рекурсивно копирует все вложенные объекты.
     ```python
     deep_copy = copy.deepcopy(original)
     ```

4. **Что такое декораторы и как они используются?**
   - **Декораторы** — это функции, которые принимают другую функцию и возвращают новую функцию с дополнительным поведением.
   - Декоратор — это функция, которая возвращает другую функцию. Декораторы применяются для того, чтобы изменить поведение некоторой функции или метода, не изменяя их код.
     ```python
     def my_decorator(func):
         def wrapper():
             print("Что-то выполняется до вызова функции.")
             func()
             print("Что-то выполняется после вызова функции.")
         return wrapper

     @my_decorator
     def say_hello():
         print("Привет!")

     say_hello()
     ```
   - Используются для добавления функциональности к существующим функциям или методам без изменения их кода.

5. **Как работают генераторы и чем они отличаются от списковых включений (list comprehensions)?**
   - **Генераторы** — это функции, которые используют `yield` для возвращения значений по одному за раз, сохраняя состояние между вызовами.
     ```python
     def my_generator():
         yield 1
         yield 2
         yield 3

     gen = my_generator()
     for value in gen:
         print(value)
     ```
   - **Списковые включения (list comprehensions)** создают и возвращают весь список сразу.
     ```python
     squares = [x**2 for x in range(10)]
     ```
   - Генераторы лениво вычисляют значения по мере необходимости, а списковые включения создают весь список в памяти сразу.

6. **Как работает контекстный менеджер (context manager) в Python?**
   - **Контекстный менеджер** управляет ресурсами через методы `__enter__` и `__exit__`.
     ```python
     with open('file.txt', 'r') as file:
         content = file.read()
     ```
   - Метод `__enter__` выполняется при входе в контекст (`with`), а `__exit__` — при выходе. Это позволяет гарантировать освобождение ресурсов, даже если внутри контекста произойдет ошибка.

7. **Что такое выражение lambda и когда его следует использовать?**
   - **Lambda** — это небольшая анонимная функция, которая определяется с использованием ключевого слова `lambda`.
     ```python
     add = lambda x, y: x + y
     print(add(2, 3))  # Output: 5
     ```
   - Используется для создания коротких функций на месте, например, в качестве аргумента для функций высшего порядка, таких как `map`, `filter`, и `sorted`.

 ### Еще пример использования **Lambda function**
 -  Example filter with lambda expression.

 ### filter
 filter(function, iterable) # function must return True or False
 ```python
 input_list = ['Delhi', 'Mumbai', 'Noida, 'Gurugram']
 to_match = 'Gurugram'
 
 matched_list = list(filter(lambda item: item == to_match, input_list))
 matched_list # ['Gurugram']
 ```
For every single item in the input_list, the condition is checked in the lambda function which returns either True or False.


8. **Как вы работаете с исключениями и как создаете свои собственные исключения?**
   - **Обработка исключений**:
     ```python
     try:
         result = 10 / 0
     except ZeroDivisionError:
         print("Деление на ноль недопустимо")
     finally:
         print("Этот блок выполняется всегда")
     ```
   - **Создание собственных исключений**:
     ```python
     class MyCustomError(Exception):
         pass

     try:
         raise MyCustomError("Произошла ошибка")
     except MyCustomError as e:
         print(e)
     ```
   - Обработка исключений позволяет контролировать поведение программы в случае ошибок, а создание собственных исключений помогает в реализации специфичных для приложения ошибок.

Эти вопросы и ответы помогут вам подготовиться к собеседованию на позицию Automation QA Python в OZON, продемонстрировав ваши знания и опыт в области программирования на Python и автоматизации тестирования.
