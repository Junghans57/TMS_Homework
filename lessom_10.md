## Задание 1
1) Установил vim:
   ```bash
   sudo apt install vim -y
   ```
2) Создал директорию practice и перешел в нее:
   ```bash
   mkdir practice
   ```
   ```bash
   cd practice
   ```
3) Создал файл memo:
   ```bash
   vim memo
   ```
4) Перешел в режим "Ввода":
   ```text
   i
   ```
5) Ввел текст:
   ```text
   @REM AUTOEXEC.BAT DTK 386/40
   ECHO OFF
   Path c:\dos;c:\stacker;c:\Util;c:\NC;C:\MOUSE
   SET PROMPT=$P$G
   SET TMP=C:\TEMP
   LH C:\UTIL\RKEGA
   goto %config%
   :student1
   C:\DOS\SMARTDRV.EXE C+ 2048 1024
   goto nc
   :student2
   APPEND E:\tc\bgi
   :teacher
   PATH %path%E:\windows;e:\tc;e:\tc\bin;e:\foxpro;
   goto win
   :ONC
   PATH %path%G:\pctcp;
   SET TZ=GMT
   goto nc
   :nc
   nc.exe
   goto end
   win.com
   :end
   ```
6) Перешел в "Командный режим":
   ```text
   Esc
   ```
7) Сохранил файл и вышел из него:
   ```text
   :wq
   ```
8) Проверил что в файле появились записи:

   <img width="404" height="458" alt="image" src="https://github.com/user-attachments/assets/ca28cb13-dc4c-47f6-89bc-15f8fc0308ba" />
## Задание 2
1) Открыл файл memo:
   ```bash
   vim memo
   ```
2) Отредактировал файл.
3) Сохранил файл и вышел из него:
   ```text
   :wq
   ```
4) Проверил что файл изменился:

<img width="466" height="531" alt="image" src="https://github.com/user-attachments/assets/152bb669-14bd-45dc-ad0d-86465411a51f" />


## Задание 3
1) Вернулся в домашний каталог:
   ```bash
   cd ..
   ```
2) Создал файл testcase.c в домашнем каталоге и скопировал в него [текст](https://gist.github.com/AnastasiyaGapochkina01/9544aee4c5d745a6002ba39c6c71b38d).
3) Открыл файл testcase.c:
   ```bash
   vim testcase.c
   ```
4) Включил отображение номеров строк:
   ```bash
   :set number
   ```
   <img width="545" height="217" alt="image" src="https://github.com/user-attachments/assets/b7b5e712-00aa-4a24-872b-0563af4a82e3" />
  
5) Заменил слово WORD на IGNORE:
   ```bash
   :%s/WORD/IGNORE/gc
   ```
6) Заменил слово Reset на set:
   ```bash
   :%s/Reset/set/gc
   ```
7) Заменил слово input на output:
   ```bash
   :%s/input/output/gc
   ```
8) Скопировал строки с 16 по 29 в файл printwords.c:
   ```bash
   :16,29y
   ```
   ```bash
   :sp printwords.c
   ```
   ```bash
   p
   ```
   ```bash
   :wq
   ```
9) Удалил 2 последние строки:
   ```bash
   2dd
   ```
10) Перенес фрагмент текста:
    ```bash
    9dd
    ```
    ```bash
    p
    ```
11) Запишисал изменения в файл testvim.c:
    ```bash
    :sav testvim.c
    ```
12) Вышел из редактора:
    ```text
    :q!
    ```
13) Проверил что файл testcase.c не изменился:
<img width="540" height="1288" alt="image" src="https://github.com/user-attachments/assets/65ff36a9-33ee-463f-868a-49937cfec9cb" />
<img width="486" height="368" alt="image" src="https://github.com/user-attachments/assets/cf6ffe74-23bb-44c0-9ad3-2321c8d05146" />






## Задание 4
1) Установил nginx:
   ```bash
   sudo apt install nginx -y
   ```
2) Проверил что nginx запущен:
  <img width="938" height="337" alt="image" src="https://github.com/user-attachments/assets/8c43e28d-1ea1-4684-a87b-829c784a4139" />

  <img width="866" height="94" alt="image" src="https://github.com/user-attachments/assets/0dead0d1-b130-4753-b6b1-1b07cd6fc422" />


3) Посмотрел логи nginx:

  <img width="668" height="198" alt="image" src="https://github.com/user-attachments/assets/04428d04-57c0-4cda-8b95-7e05c89affc2" />


5) Посмотрел уровень нагрузки на ОС:
   ```bash
   htop
   ```
  <img width="948" height="344" alt="image" src="https://github.com/user-attachments/assets/20536679-2b0a-485e-b3d0-079fcf0765c1" />


6) Посмотрел логи действий пользователей системы:
   ```bash
   sudo journalctl -b
   ```
  <img width="1380" height="287" alt="image" src="https://github.com/user-attachments/assets/faea57ae-60cf-4b64-954a-6a7931e4f406" />

