## Задание 1
1) Создал text_file.txt:
   
   ```text
   Он --- серо-буро-малиновая редиска!!
   >>>:->
   А не кот.
   www.kot.ru
   ```

2) Сделал скрипт words-counter.sh:

   ```bash
   FILE_FOR_SEARCH="$1"

   # Check if file exists
   if [ ! -f "${FILE_FOR_SEARCH}" ]; then
     echo "Usage: $0 file"
     exit 1
   fi

   # Search mathces and put to array
   matches_arr=($(grep -o -P '(?:[а-яА-Яa-zA-Z]+-|(?:[а-яА-Яa-zA-Z]))+' ${FILE_FOR_SEARCH}))

   # Print number of matches to cli
   echo -e "Number of matches: ${#matches_arr[@]}\n"

   # Print each match to cli
   counter=1
   for match in ${matches_arr[@]}; do
     echo "Match ${counter}: $match"
     ((counter++))
   done
   ```

3) Запустил скрипт:

<img width="451" height="251" alt="image" src="https://github.com/user-attachments/assets/083f4fe5-f93c-47fb-bb08-80ee62f56a2e" />

## Задание 2
1) Создал каталоги с файлами:

  <img width="476" height="72" alt="image" src="https://github.com/user-attachments/assets/5c15ee7b-bd0d-4eba-8c33-b458f6137442" />

2) Создал локальный репозиторий:

   ```text
   git init
   ```

3) Добавил файлы в индекс и сделал коммит:

   ```text
   git add .
   ```
   ```text
   git commit -m "First commit"
   ```

4) Получил инфо по коммиту:

<img width="516" height="105" alt="image" src="https://github.com/user-attachments/assets/92959e51-3226-4cb2-97bf-7bedcc082002" />

5) Сделал скрипт change-filenames.sh:

   ```bash
   set -ue

   WORK_FOLDER="$1"

   # Check if folder exists
   if [ ! -d "$WORK_FOLDER" ]; then
     echo "Usage: $0 folder"
     exit 1
   fi

   find_files_with_ext() {
     local EXTENTION="$1"

     cd "$PWD"
     find "$WORK_FOLDER" -type f -name "*.${EXTENTION}";
   }

   rename_files() {
     local -n FILES_ARR="$1"
     local NEW_FILES_TEMPLATE="$2"

     cd "$PWD"
     for path in "${FILES_ARR[@]}"; do
       local filename_with_ext=$(basename $path)
       local filename_without_ext=$(echo "${filename_with_ext}" | sed -E 's/\.[a-z]+$//')
       local dirname=$(dirname $path)
       local new_file_template_result=${NEW_FILES_TEMPLATE/filename_without_ext/${filename_without_ext}}

       mv "$path" "${dirname}/${new_file_template_result}"
     done
   }

   # Get last commit timestamp
   PWD=$(pwd)
   cd "$WORK_FOLDER"
   # Check if commit exists
   if ! COMMIT_TIMESTAMP=$(git log -1 --format=%ct 2>/dev/null); then
     echo "Commit does not exist"
     exit 1
   fi

   # Find .log files and put to array
   log_files_arr=($(find_files_with_ext "log"))

   # Check if .log files exists
   if [ "${#log_files_arr[@]}" -ne 0 ]; then

     # Add commit timestamp to filenames .log files
     rename_files log_files_arr "filename_without_ext_${COMMIT_TIMESTAMP}.log"
   fi

   # Get last commit hash
   cd "$WORK_FOLDER"
   COMMIT_HASH=$(git rev-parse --short HEAD)

   # Find .py files and put to array
   py_files_arr=($(find_files_with_ext "py"))

   # Check if .py files exists
   if [ "${#py_files_arr[@]}" -ne 0 ]; then

     # Add commit hash to filenames .py files
     rename_files py_files_arr "filename_without_ext_${COMMIT_HASH}.py"
   fi
   ````

6) Выполнил скрипт:

<img width="955" height="174" alt="image" src="https://github.com/user-attachments/assets/e41ba3a0-166d-4049-857d-382659707396" />


## Задание 3
1) Создал text_file.txt:
   
   ```text
   Довольно распространённая ошибка ошибка - это лишний повтор повтор слова  слова. Смешно, не правда ли? Не нужно портить хор хоровод.
   ```

2) Сделал скрипт erase-dublicates.sh:

   ```bash
   FILE_FOR_SEARCH="$1"

   # Check if file exists
   if [ ! -f "${FILE_FOR_SEARCH}" ]; then
     echo "Usage: $0 file"
     exit 1
   fi

   # Print text without dublicates t cli
   echo "$(sed -E 's/\b(\w+)\s+\1\b/\1/g' "$FILE_FOR_SEARCH")"
   ```

3) Запустил скрипт:

  <img width="896" height="36" alt="image" src="https://github.com/user-attachments/assets/c6da8161-41ad-4f8a-b2f9-b11f5b5fe123" />
