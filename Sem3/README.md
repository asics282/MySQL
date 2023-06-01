```sql
# Создаем новую БД
CREATE DATABASE hw3;

# выбор бд для работы
USE hw3;

# создание сущности (таблица salespeople)
CREATE TABLE salespeople
(
    snum INT PRIMARY KEY AUTO_INCREMENT NOT NULL,
    sname VARCHAR(100) NOT NULL,
    city VARCHAR(100) NOT NULL,
    comm VARCHAR(50)
);

# создание сущности (таблица customers, зависимая от salespeople)
CREATE TABLE customers
(
    cnum INT PRIMARY KEY NOT NULL,
    cname VARCHAR(100) NOT NULL,
    city VARCHAR(100) NOT NULL,
    rating INT NOT NULL,
    snum INT, 
    FOREIGN KEY (snum) REFERENCES salespeople (snum) # внешний ключ
);

# создание сущности (таблица orders, зависимая от salespeople)
CREATE TABLE orders
(
    onum INT PRIMARY KEY NOT NULL,
    atm FLOAT(7,2) NOT NULL CHECK (atm > 0), # c ограничением для диапазона значений, которые могут храниться в столбце (все положительные)
    odate DATE NOT NULL,
    cnum INT,
    snum INT,
    FOREIGN KEY (cnum) REFERENCES customers (cnum), # внешний ключ
    FOREIGN KEY (snum) REFERENCES salespeople (snum) # внешний ключ
);

CREATE TABLE workers
(
    id INT PRIMARY KEY AUTO_INCREMENT NOT NULL,
    name VARCHAR(45) NOT NULL,
    surname VARCHAR(45) NOT NULL,
    specialty VARCHAR(45) NOT NULL,
    seniority INT,
    salary INT,
    age INT
);

# заполнение таблиц данными
INSERT INTO salespeople (snum, sname, city, comm)
VALUES
(1001, 'Peel', 'London', '.12'),
(1002, 'Serres', 'San Jose', '.13'),
(1004, 'Motika', 'London', '.11'),
(1007, 'Rifkin', 'Barcelona', '.15'),
(1003, 'Axelrod', 'New York', '.10');

INSERT INTO customers (cnum, cname, city, rating, snum)
VALUES
(2001, 'Hoffman', 'London', 100, 1001),
(2002, 'Giovanni', 'Rome', 200, 1003),
(2003, 'Liu', 'SanJose', 200, 1002),
(2004, 'Grass', 'Berlin', 300, 1002),
(2006, 'Clemens', 'London', 100, 1001),
(2008, 'Cisneros', 'London', 100, 1001),
(2007, 'Pereira', 'Rome', 100, 1004);

INSERT INTO orders (onum, atm, odate, cnum, snum)
VALUES
(3001, 18.69, '1990-03-10', 2008, 1007),
(3003, 767.19, '1990-03-10', 2001, 1001),
(3002, 1900.10, '1990-03-10', 2007, 1004),
(3005, 5160.45, '1990-03-10', 2003, 1002),
(3006, 1098.16, '1990-03-10', 2008, 1007),
(3009, 1713.23, '1990-04-10', 2002, 1003),
(3007, 75.75, '2016-01-01', 2004, 1002),
(3008, 4723.00, '1990-04-10', 2006, 1001),
(3010, 1309.95, '2016-01-01', 2004, 1002),
(3011, 9891.88, '2016-01-01', 2006, 1001);

INSERT INTO workers (id, name, surname, specialty, seniority, salary, age)
VALUES
(1,'Вася', 'Васькин', 'начальник', 40, 100000, 60),
(2,'Петя', 'Петькин', 'начальник', 8, 70000, 30),
(3,'Катя', 'Каткина', 'инженер', 2, 70000, 25),
(4,'Саша', 'Сашкин', 'инженер', 12, 50000, 35),
(5,'Иван', 'Иванов', 'рабочий', 40, 30000, 59),
(6,'Петр', 'Петров', 'рабочий', 20, 25000, 40),
(7,'Сидор', 'Сидоров', 'рабочий', 10, 20000, 35),
(8,'Антон', 'Антонов', 'рабочий', 8, 19000, 28),
(9,'Юра', 'Юркин', 'рабочий', 5, 15000, 25),
(10,'Максим', 'Воронин', 'рабочий', 2, 11000, 22),
(11,'Юра', 'Галкин', 'рабочий', 3, 12000, 24),
(12,'Люся', 'Люськина', 'рабочий', 10, 10000, 49),
(13, 'Жорик', 'Иванов', 'уборщик', 4, 12000, 35);
```
![Таблица salespeople](/Sem3/salespeople.png)

![Таблица customers](/Sem3/customers.png)

![Таблица orders](/Sem3/orders.png)

![Таблица workers](/Sem3/workers.png)

# Задание №1
1. Напишите запрос, который вывел бы таблицу со столбцами в следующем порядке: city, sname, snum, comm. (к первой или второй таблице, используя SELECT)

```sql
SELECT city, sname, snum, comm FROM salespeople;
```

2. Напишите команду SELECT, которая вывела бы оценку(rating), сопровождаемую именем каждого заказчика в городе San Jose. (“заказчики”)

```sql
SELECT rating 'Рейтинг', cname 'Имя', city FROM customers WHERE city = 'SanJose';
```

3. Напишите запрос, который вывел бы значения snum всех продавцов из таблицы заказов без каких бы то ни было повторений. (уникальные значения в “snum“ “Продавцы”)

```sql
SELECT DISTINCT snum FROM salespeople;
```
4. Напишите запрос, который бы выбирал заказчиков, чьи имена начинаются с буквы G. Используется оператор "LIKE": (“заказчики”)

```sql
SELECT * FROM customers WHERE cname LIKE 'G%';
```

5. Напишите запрос, который может дать вам все заказы со значениями суммы выше чем $1,000. (“Заказы”, “amt” - сумма)

```sql
SELECT * FROM orders WHERE atm > 4000;
```

6. Напишите запрос который выбрал бы наименьшую сумму заказа.

```sql
SELECT MIN(snum) AS 'Минимальный заказ' FROM orders;
```

7. Напишите запрос к таблице “Заказчики”, который может показать всех заказчиков, у которых рейтинг больше 100 и они находятся не в Риме.

```sql
SELECT * FROM customers WHERE rating > 100 AND city != 'Rome';
```

# Задание №2
1. Отсортируйте поле “зарплата” в порядке убывания и возрастания

```sql
SELECT * FROM workers ORDER BY salary;
SELECT * FROM workers ORDER BY salary DESC;
```

2. Отсортируйте по возрастанию поле “Зарплата” и выведите 5 строк с наибольшей заработной платой (возможен подзапрос)

```sql
SELECT * FROM workers ORDER BY salary DESC LIMIT 5;
```

3. Выполните группировку всех сотрудников по специальности, суммарная зарплата которых превышает 100000

```sql
SELECT sum(salary) salary, specialty specialty FROM workers
GROUP BY specialty HAVING salary > 100000;
```