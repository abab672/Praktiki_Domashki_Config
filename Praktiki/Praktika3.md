# Практика 3
## Задача 1
Реализовать на Jsonnet приведенный ниже пример в формате JSON. Использовать в реализации свойство программируемости и принцип DRY.

```
local groups = [
  "ИКБО-1-24",
  "ИКБО-2-24",
  "ИКБО-3-24",
  "ИКБО-4-24",
  "ИКБО-5-24",
  "ИКБО-6-24",
  "ИКБО-7-24",
  "ИКБО-8-24",
  "ИКБО-9-24",
  "ИКБО-10-24",
  "ИКБО-11-24",
  "ИКБО-12-24",
  "ИКБО-13-24",
  "ИКБО-14-24",
  "ИКБО-15-24",
  "ИКБО-16-24",
  "ИКБО-17-24",
  "ИКБО-18-24",
  "ИКБО-19-24",
  "ИКБО-20-24",
  "ИКБО-21-24",
  "ИКБО-22-24",
  "ИКБО-23-24",
  "ИКБО-24-24",
  "ИКБО-52-23"
];

local student(name, age, group, subject) = {
  name: name,
  age: age,
  group: group,
  subject: subject,
};

local students = [
  student("Иванов И.И.", 19, "ИКБО-4-24", "Конфигурационное управление"),
  student("Петров П.П.", 18, "ИКБО-5-24", "Конфигурационное управление"),
  student("Сидоров С.С.", 18, "ИКБО-5-24", "Конфигурационное управление"),
  student("Бутаев А.А.", 18, "ИКБО-52-23", "Конфигурационное управление")
];

{
  groups: groups,
  students: students,
}
```

### Решение:
1)  Устанавливаем jsonnet

```
sudo apt install jsonnet
```

2)  Создаем файл prakt3.jsonnet, добавляем в него код из условия и компилируем файл в json

![3pr1task](https://github.com/user-attachments/assets/60cf0fcd-0bb8-437f-906f-988482129dc1)



## Задача 2
Реализовать на Dhall приведенный выше пример в формате JSON. Использовать в реализации свойство программируемости и принцип DRY.

### Решение:
1) Устанавливаем Dhall

```
sudo apt install dhall
```

2) Создаем файл pr3_t2.dhall и добавляем в него следующий код

```
let Group = Text
let Student = { age : Natural, group : Group, name : Text }

let create_student : Natural -> Text -> Text -> Student =
  \(age : Natural) -> \(group : Text) -> \(name : Text) ->
  { age = age, group = group, name = name }

let create_group : Natural -> Group =
  \(num : Natural) ->
  "ИКБО-" ++ (Natural/show num) ++ "-24"

let groups : List Group = [ 
  create_group 1,
  create_group 2,
  create_group 3,
  create_group 4,
  create_group 5,
  create_group 6,
  create_group 7,
  create_group 8,
  create_group 9,
  create_group 10,
  create_group 11,
  create_group 12,
  create_group 13,
  create_group 14,
  create_group 15,
  create_group 16,
  create_group 17,
  create_group 18,
  create_group 19,
  create_group 20,
  create_group 21,
  create_group 22,
  create_group 23,
  create_group 24,
  create_group 52,
]

let students : List Student = [ 
  create_student 19 (create_group 4) "Иванов И.И.", 
  create_student 18 (create_group 4) "Петров П.П.",
  create_student 18 (create_group 5) "Сидоров С.С.",
  create_student 18 (create_group 52) "Бутаев А.А."
]

let subject = "Конфигурационное управление"

in { groups = groups, students = students, subject = subject }
```

3) Меняем формат на json с помощью

```
dhall-to-json <pr3_t2.dhall> pr3_t2.json
```
4) Выводим результат
```
cat pr3_t2.json
```

![image](https://github.com/user-attachments/assets/362e08dd-6188-46f0-b797-6337eedddda7)


# _____________________________________________________________
Для решения дальнейших задач потребуется программа на Питоне, представленная ниже. Разбираться в самом языке Питон при этом необязательно.

```Python
import random


def parse_bnf(text):
    '''
    Преобразовать текстовую запись БНФ в словарь.
    '''
    grammar = {}
    rules = [line.split('=') for line in text.strip().split('\n')]
    for name, body in rules:
        grammar[name.strip()] = [alt.split() for alt in body.split('|')]
    return grammar


def generate_phrase(grammar, start):
    '''
    Сгенерировать случайную фразу.
    '''
    if start in grammar:
        seq = random.choice(grammar[start])
        return ''.join([generate_phrase(grammar, name) for name in seq])
    return str(start)


BNF = '''
E = a
'''

for i in range(10):
    print(generate_phrase(parse_bnf(BNF), 'E'))

```

Реализовать грамматики, описывающие следующие языки (для каждого решения привести БНФ). Код решения должен содержаться в переменной BNF:
# _____________________________________________________________



## Задача 3
Язык нулей и единиц

### Решение
```python
BNF = '''
E = 0 | 1 E | 1
'''
```

![image](https://github.com/user-attachments/assets/09740216-00f4-40b4-81c2-d3f7a95ec5ab)



## Задача 4
Язык правильно расставленных скобок двух видов

### Решение
```python
BNF = '''
E = () | {} | ( E ) | { E } | E E
'''
```
![image](https://github.com/user-attachments/assets/cee638a5-e120-4bd5-8ffc-4cf9f8071c5a)



## Задача 5
Язык выражений алгебры логики

### Решение
```python
BNF = '''
E = ( E B F ) | U ( E ) | F
F = P B P | U P | P
P = x | y | (x) | (y)
U = ~
B = & | V
'''
```

![image](https://github.com/user-attachments/assets/bad161c9-2266-4329-97b9-6cb0081a8bdd)
