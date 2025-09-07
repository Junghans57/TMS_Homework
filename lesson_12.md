## Задание 1
1) Создал каталог:

  <img width="379" height="70" alt="image" src="https://github.com/user-attachments/assets/6c0b75ad-bbd1-4aab-be0d-ec30477d00ff" />


## Задание 2
1) Установил инструменты для компиляции:

   ```bash
   sudo apt install -y build-essential
   ```

2) Создал файл 1.c:

   ```c
   #include <stdio.h>

   int main() {
     printf("HELLO Ubuntu\n");

     return 0;
   }
   ```

3) Скомпилировал:

  <img width="375" height="54" alt="image" src="https://github.com/user-attachments/assets/ed55a189-856a-4303-87c3-3c85325ff226" />

4) Запустил:

<img width="299" height="30" alt="image" src="https://github.com/user-attachments/assets/3a6f1ffb-9338-47df-895d-2c19fb5612eb" />


## Задание 3
1) Создал Bash-скрипт args.sh

   ```bash
   # Print args to cli
   echo "Arguments: $@"

   # Check if file exists
   FILE_WITH_ARGUMENTS="arguments.txt"
   if [ ! -f "$FILE_WITH_ARGUMENTS" ]; then
     touch "$FILE_WITH_ARGUMENTS"
   fi

   # Print args to file
   echo "Arguments: $@" > "$FILE_WITH_ARGUMENTS"
   ```
2) Запустил скрипт:

<img width="557" height="71" alt="image" src="https://github.com/user-attachments/assets/b3c55b6d-b221-4c80-a83f-41edcfb5b321" />



## Задание 4
1) Создал каталоги и файлы:


2) Создал скрипт list_files.sh:
   ```bash
   #!/bin/bash
   # $1 - имя файла для вывода
   # $2 - каталог, где искать
   # $3 - расширение файлов

   output_file="$1"
   directory="$2"
   extension="$3"

   # Находим файлы и записываем в файл
   find "$directory" -type f -name "*.$extension" > "$output_file"
   echo "Список файлов с расширением .$extension записан в $output_file"

                                                                                
   ```

3) Запустил скрипт 1й раз:

  <img width="772" height="71" alt="image" src="https://github.com/user-attachments/assets/c37d1da5-2695-4897-918e-80bdaf099928" />


4) Запустил скрипт 2й раз:

   <img width="1116" height="136" alt="image" src="https://github.com/user-attachments/assets/ec35e3a2-712d-46ee-ab82-8a98f6182ceb" />

5) Запустил скрипт 3й раз:

   <img width="1099" height="136" alt="image" src="https://github.com/user-attachments/assets/9c9102a8-f0f3-44fd-b7e1-a87cd6ea8e2f" />

## Задание 5
1) Создал скрипт show-sizes-and-rules-for-files.sh:

   ```bash
   set -u

   # Check args length
   if [ ${#} -ne 1 ]; then
     echo "Usage: ${0} folder"
     exit 1
   fi

   # Check if folder
   if [ ! -d ${1} ]; then
     echo "Error: it isn't a folder"
     exit 1
   fi

   FOLDER_TO_SEARCH="$1"

   # Find files and put in array
   files_arr=($(find "$FOLDER_TO_SEARCH" -type f))

   # Print rules, sizes and filenames to cli
   for file in ${files_arr[@]}; do
     ls -lh ${file} | awk '{print $1,"\t"$5,"\t"$9}'
   done
   ```

2) Запустил скрипт:

   <img width="946" height="357" alt="image" src="https://github.com/user-attachments/assets/63ec3566-48fe-4024-9841-221ecfe3b3cb" />
