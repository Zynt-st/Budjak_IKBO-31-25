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
nano check comment
chmod +x check comment
./check comment hello.c
```

```
#!/bin/bash
file="$1"

# Достаём первую строку из файла
first_line=$(head -n 1 "$file")

# Проверяем расширение файла и наличие комментария в первой строке
if [[ "$file" == *.c ]] || [[ "$file" == *.js ]]; then
    if echo "$first_line" | grep -q -E "^([[:space:]]*//|[[:space:]]*/\*)"; then
        echo "В первой строке есть комментарий"
    else
        echo "В первой строке нет комментария"
    fi
elif [[ "$file" == *.py ]]; then
    if echo "$first_line" | grep -q -E "^[[:space:]]*#"; then
        echo "В первой строке есть комментарий"
    else
        echo "В первой строке нет комментария"
    fi
else
    echo "Неизвестное расширение файла (поддерживаются только .c, .js, .py)"
fi
```

Задание 7
Написать программу для нахождения файлов-дубликатов (имеющих 1 или более копий содержимого) по заданному пути (и подкаталогам).
```
nano find_duplicates
chmod +x find_duplicates
./find_duplicates
```

```
#!/bin/bash
dir="${1:-.}"
find "$dir" -type f -exec md5sum {} + | sort | uniq -w 32 -d --all-repeated=separate
```

Задача 8
Написать программу, которая находит все файлы в данном каталоге с расширением, указанным в качестве аргумента и архивирует все эти файлы в архив tar.
```
nano archive_files
chmod +x archive_files
./archive_files c
```

```
#!/bin/bash
ext="$1"
tar -cvf archive.tar *."$ext"
```

Задача 9
Написать программу, которая заменяет в файле последовательности из 4 пробелов на символ табуляции. Входной и выходной файлы задаются аргументами.
```
nano spaces_to_tabs
chmod +x spaces_to_tabs
./spaces_to_tabs input. txt output. txt
cat output. txt
```

```
#!/bin/bash
sed 's/    /\t/g' "$1" > "$2"
```

Задача 10
Написать программу, которая выводит названия всех пустых текстовых файлов в указанной директории. Директория передается в программу параметром.
```
nano find_empty
chmod +x find_empty
./find_empty test_folder
```

```
#!/bin/bash
find "$1" -maxdepth 1 -type f -empty
```
