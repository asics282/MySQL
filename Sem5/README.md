![MySQL](/Sem4/Mysql.png)

# Представления

```sql
# Создаем новую БД
CREATE DATABASE hw5;

# выбор бд для работы
USE hw5;

# создание сущности (таблица AUTO)
CREATE TABLE AUTO (
	id INT auto_increment PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    cost decimal (10, 2)
);

# заполнение таблицы данными

INSERT INTO auto (name, cost)
VALUES
('Audi', 52642.00),
('Mersedes', 57127.00),
('Skoda', 9000.00),
('Volvo', 29000.00),
('Bently', 350000.00),
('Citroen', 21000.00),
('Hummer', 41400.00),
('Volkswagen', 21600.00);
```
![Таблица AUTO](/Sem5/AUTO.png)

### 1. Создайте представление, в которое попадут автомобили стоимостью до 25 000 долларов

```sql
CREATE VIEW cars AS 
SELECT * 
FROM auto 
WHERE cost < 25000.00;
```

### 2. Изменить в существующем представлении порог для стоимости: пусть цена будет до 30 000 долларов (используя оператор ALTER VIEW)

```sql
ALTER VIEW cars AS 
SELECT * 
FROM auto 
WHERE cost > 30000.00;
```

### 3. Создайте представление, в котором будут только автомобили марки “Шкода” и “Ауди” (аналогично)

```sql
ALTER VIEW carsn AS 
SELECT * 
FROM auto 
WHERE name IN('Skoda', 'AUDI');
```