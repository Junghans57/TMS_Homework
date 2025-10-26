<h2>Цель: Практически применить изученные темы: функции, работу с
файлами и директориями, а также шаблонизатор Jinja</h2>
Задание:
<ol>
<li>Напишите функцию multiply_numbers(), которая принимает два
аргумента и возвращает их произведение. Затем вызовите эту функцию
и выведите результат на экран.</li> 

    def multiply_numbers(a, b):
    return a*b

result = multiply_numbers(3, 9)
print(result)
***
    python3 multiply_numbers.py 
    27
<li>Создайте файл test.txt и запишите в него строку "Это тестовый файл для
домашнего задания по программированию". Затем откройте этот файл в
режиме чтения, прочитайте его содержимое и выведите на экран.</li>

   file_name="text.txt"

with open(file_name, "w") as f:
    f.write("Это тестовый файл")

with open(file_name, "r") as f:
    print(f.read())
***
    python3 testtxt.py
    Это тестовый файл
<li>Создайте пустую директорию mydir в текущей рабочей директории.
Затем перейдите в эту директорию и создайте в ней три пустых файла:
file1.txt, file2.txt и file3.txt. Наконец, выведите список файлов в
директории на экран.</li>

    import os

    os.mkdir("mydir")

    os.chdir("mydir")

    for name in ["file1.txt", "file2.txt", "file3.txt"]:
    open(name, "w").close()

    print("Файлы в директории:", os.listdir())
***
   <img width="618" height="41" alt="image" src="https://github.com/user-attachments/assets/efc3c555-613c-4ef8-8b12-f6628c76ae96" />

***
   <img width="598" height="153" alt="image" src="https://github.com/user-attachments/assets/c795d039-94e0-4980-a669-3e0a70b9d514" />

<li>Создайте шаблон template.html, который будет содержать HTML-код
для отображения списка пользователей. Шаблон должен использовать
цикл for для перебора элементов списка, и выводить имя и email
каждого пользователя. Затем создайте список пользователей в виде
списка словарей, передайте его в шаблон и отобразите результат на
экране.</li> 
template.htm:

    <!DOCTYPE html>
    <html lang="ru">
    <head>
       <meta charset="UTF-8">
       <title>Список пользователей</title>
    </head>
    <body>
       <h1>Пользователи</h1>
       <ul>
       {% for user in users %}
          <li>{{ user.name }} — {{ user.email }}</li>
       {% endfor %}
      </ul>
    </body>
    </html>

render_template.py:

    from jinja2 import Environment, FileSystemLoader

    env = Environment(loader=FileSystemLoader('.'))
    template = env.get_template('template.html')

    users = [
      {"name": "Андрей", "email": "andrey@example.com"},
      {"name": "Мария", "email": "maria@example.com"},
      {"name": "Иван", "email": "ivan@example.com"}
    ]

    output = template.render(users=users)

    with open("output.html", "w", encoding="utf-8") as f:
      f.write(output)

    print("✅ HTML-файл создан: output.html")
Out:

    <!DOCTYPE html>
    <html lang="ru">
    <head>
      <meta charset="UTF-8">
      <title>Список пользователей</title>
    </head>
    <body>
      <h1>Пользователи</h1>
      <ul>
          <li>Андрей — andrey@example.com</li>
          <li>Мария — maria@example.com</li>
          <li>Иван — ivan@example.com</li>
      </ul>
    </body>
    </html>
