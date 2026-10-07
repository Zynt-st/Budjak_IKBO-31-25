Задача 1
Вывести отсортированный в алфавитном порядке список имен пользователей в файле passwd.
```
grep -o "^[^:]*" passwd | sort
```

Задача 2
Вывести данные /etc/protocols в отформатированном и отсортированном порядке для 5 наибольших портов.
```
grep -v "^#" /etc/protocols | sort -k2 -n -r | head -5
```

Задача 3
Написать программу banner средствами bash для вывода текстов.
```
nano banner
chmod +x bammer
./banner "Hello from RTU MIREA!"
```

```
#!/bin/bash
text="$1"
len=${#text}

line="+"
for ((i=0; i<len+2; i++)); do
    line="${line}-"
done
line="${line}+"

echo "$line"
echo "| $text |"
echo "$line"
```

Задача 4
Написать программу для вывода всех идентификаторов в файле.
```
nano identifiers
chmod +x identifiers
./identifiers hello.c
```

```
#!/bin/bash
grep -o -E "[a-zA-Z_][a-zA-Z0-9_]*" "$1" | sort -u | tr '\n' ' '
echo
```

Задание 5
Написать программу для регистрации пользовательской команды.
```
nano reg
chmod +x reg
sudo ./reg banner
ls -l /usr/local/bin
banner "Hello world"
```

```
#!/bin/bash
chmod +x "$1"
cp "$1" /usr/local/bin/
```

Задание 6
Написать программу для проверки наличия комментария в первой строке файлов с расширениями c, js и py.
```
