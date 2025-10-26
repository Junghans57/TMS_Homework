<h2>Цель: Практически применить изученные темы: ООП, классы и ООП в
Python.</h2>
Задание:
<ol>
<li>Создайте класс "Круг", который имеет атрибуты радиус и цвет, и
методы вычисления площади и длины окружности. Создайте несколько
объектов этого класса и вызовите его методы для каждого объекта.</li>

    import math

    class Circle:
        def __init__(self, radius, color):
            self.radius = radius
            self.color = color

        def area(self):
            return math.pi * self.radius ** 2

        def circumference(self):
            return 2 * math.pi * self.radius

    circle1 = Circle(5, "red")
    circle2 = Circle(10, "blue")

    print(f"Круг 1: площадь = {circle1.area():.2f}, длина окружности = {circle1.circumference():.2f}")
    print(f"Круг 2: площадь = {circle2.area():.2f}, длина окружности = {circle2.circumference():.2f}")

***
  <img width="537" height="65" alt="image" src="https://github.com/user-attachments/assets/c355b29f-8c45-4f67-a660-038f5b7e808c" />

<li>Создайте класс "Банковский счет", который имеет атрибуты номер
счета, имя владельца, баланс и методы пополнения и снятия денег со
счета. Создайте несколько объектов этого класса и вызовите его методы
для каждого объекта.</li>

    class BankAccount:
    def __init__(self, account_number, owner_name, balance=0):
        self.account_number = account_number
        self.owner_name = owner_name
        self.balance = balance

    def deposit(self, amount):
        self.balance += amount
        print(f"💵 Пополнено на {amount}. Новый баланс: {self.balance}")

    def withdraw(self, amount):
        if amount <= self.balance:
            self.balance -= amount
            print(f"💸 Снято {amount}. Остаток: {self.balance}")
        else:
            print("⚠️ Недостаточно средств!")

    acc1 = BankAccount("12345", "Мaksim", 1000)
    acc1.deposit(500)
    acc1.withdraw(300)
    acc1.withdraw(2000)

***
  <img width="470" height="104" alt="image" src="https://github.com/user-attachments/assets/1f39a64e-bbfe-405d-8ca4-a66230e5d0c1" />

<li>Создайте класс "Студент", который имеет атрибуты имя, возраст и
средний балл. Создайте методы для вычисления среднего балла и
определения статуса студента (отличник, хорошист, троечник).Создайте
несколько объектов этого класса и вызовите его методы для каждого
объекта.</li>

      class Student:
    def __init__(self, name, age, grades):
        self.name = name
        self.age = age
        self.grades = grades  # список оценок

    def average_grade(self):
        return sum(self.grades) / len(self.grades)

    def status(self):
        avg = self.average_grade()
        if avg >= 9:
            return "Отличник"
        elif avg >= 7:
            return "Хорошист"
        else:
            return "Троечник"



    student1 = Student("Мaksim", 20, [10, 9, 10])
    student2 = Student("Оля", 19, [7, 8, 7])
    student3 = Student("Иван", 22, [5, 6, 6])

    for s in [student1, student2, student3]:
        print(f"{s.name}: средний балл = {s.average_grade():.1f}, статус = {s.status()}")

***
  <img width="454" height="88" alt="image" src="https://github.com/user-attachments/assets/a9226d43-08e1-45e3-8146-ed658970ffcd" />

<li>Создайте класс "Книга", который имеет атрибуты название, автор и год
издания. Создайте методы для получения и изменения этих
атрибутов.Создайте несколько объектов этого класса и вызовите его
методы для каждого объекта.</li>

     class Book:
    def __init__(self, title, author, year):
        self.title = title
        self.author = author
        self.year = year

    def get_info(self):
        return f"'{self.title}' — {self.author}, {self.year}"

    def set_year(self, new_year):
        self.year = new_year

    book1 = Book("1984", "Джордж Оруэлл", 1949)
    book2 = Book("Мастер и Маргарита", "Булгаков", 1967)

    print(book1.get_info())
    book1.set_year(1950)
    print(book1.get_info())

***
  <img width="431" height="62" alt="image" src="https://github.com/user-attachments/assets/957a4afe-d6b6-41fc-9ffd-e0a31d706258" />

<li>Создайте класс "Автомобиль", который имеет атрибуты марка, модель,
цвет и год выпуска. Создайте методы для получения и изменения этих
атрибутов. Создайте несколько объектов этого класса и вызовите его
методы для каждого объекта</li>

      class Car:
    def __init__(self, stamp, model, color, year):
        self.stamp = stamp
        self.model = model
        self.color = color
        self.year = year
    
    def car_info(self):
        print(f"Марка: {self.stamp}")
        print(f"Модель: {self.model}")
        print(f"Цвет: {self.color}")
        print(f"Год выпуска: {self.year}")
        print("-" * 30)
              
    def change_info(self, stamp=None, model=None, color=None, year=None):
        if stamp:
            self.stamp = stamp
        if model:
            self.model = model
        if color:
            self.color = color
        if year:
            self.year = year
        print("Информация обновлена")
        print("-" * 30)

    def main():
        # Создаём машины
        car1 = Car("Tesla", "Model S", "черный", 2023)
        car2 = Car("BMW", "X5", "белый", 2020)
    
        # Вывод информации о всех машинах
        print("Информация о всех машинах:")
        for car in [car1, car2]:
            car.car_info()
    
        # Меняем цвет и год первой машины
        car1.change_info(color="красный", year=2024)
        print("После изменения первой машины:")
        for car in [car1, car2]:
          car.car_info()

    if __name__ == "__main__":
    main()

***
  <img width="428" height="541" alt="image" src="https://github.com/user-attachments/assets/e9095829-025a-4526-9ea1-cc9199361389" />

</ol>
