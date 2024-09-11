# Praktiki_Domashki_Config
# <<<1 ПРАКТИКА>>>
# Задача 1
Вывести отсортированный в алфавитном порядке список имен пользователей в файле passwd (вам понадобится grep).

### Решение: 
grep '.*' /etc/passwd | cut -d: -f1 | sort  
<img width="343" alt="1zadanie" src="https://github.com/user-attachments/assets/94175a47-9734-478c-97b6-44bcd3ceebfa">



# Задача 2
Вывести данные /etc/protocols в отформатированном и отсортированном порядке для 5 наибольших портов, как показано в примере ниже:

[root@localhost etc]# cat /etc/protocols ...  
142 rohc  
141 wesp  
140 shim6  
139 hip  
138 manet  
### Решение:
cat /etc/protocols | sort -n -r -k 2 | head -n 5 | awk '{print $2" "$1}'

<img width="494" alt="2zadanie" src="https://github.com/user-attachments/assets/169a3bbc-8960-455e-ab4f-c251bfadfdd6">




# Задача 3
Написать программу banner средствами bash для вывода текстов, как в следующем примере (размер баннера должен меняться!):

[root@localhost ~]# ./banner "Hello from RTU MIREA!"  
+-----------------------+  
| Hello from RTU MIREA! |  
+-----------------------+ 
### Решение:
