1. Используя операторы языка SQL, создайте табличку “sales”. Заполните ее данными
```sql
# создание базы данных
CREATE DATABASE hw2;

# выбор бд для работы
USE hw2;

# создание сущности
CREATE TABLE sales
(
    id INT PRIMARY KEY AUTO_INCREMENT NOT NULL,
    order_date DATE NOT NULL,
    product_count INT DEFAULT '0'
);

# заполнение таблицы данными
INSERT INTO sales (order_date, product_count)
VALUES
('2023-05-22', 99),
('2023-05-23', 78),
('2023-05-24', 50),
('2023-05-25', 101),
('2023-05-26', 155),
('2023-05-27', 245),
('2023-05-28', 304),
('2023-05-29', 500),
('2023-05-30', 344);
```

2. Разделите значения поля “bucket” на 3 сегмента: меньше 100(“Маленький заказ”), 100-300 (“Средний заказ”) и больше 300 (“Большой заказ”)
```sql

# условие, да бы разделить тип заказа на 3 сегмента
SELECT id, order_date, product_count,
    CASE
        WHEN product_count < 100
            THEN 'Маленький заказ'
        WHEN (product_count > 100 AND product_count < 300)
            THEN 'Средний заказ'
        WHEN product_count > 300
            THEN 'Большой заказ'
END AS bucket
FROM sales;
```
3. Создайте таблицу “orders”, заполните ее значениями. Покажите “полный” статус заказа, используя оператор CASE
```sql
# создание новой сущности
CREATE TABLE orders
(
    order_id INT PRIMARY KEY AUTO_INCREMENT NOT NULL,
    employee_id VARCHAR(10) NOT NULL,
    amount FLOAT(7,2) NOT NULL DEFAULT '0',
    order_status VARCHAR(20) NOT NULL
);
# заполнение таблицы данными
INSERT INTO orders (employee_id, amount, order_status)
VALUES
('e3', 15.0, 'OPEN'),
('e1', 25.2, 'OPEN'),
('e5', 10.4, 'CLOSED'),
('e5', 99.99, 'OPEN'),
('e3', 78.9, 'CLOSED'),
('e4', 9.5, 'CANCELLED'),
('e4', 11.1, 'OPEN');

# условие для показа отдельной колонки 'full_order_status' с интересующими нас условиями отбора и заменой маски значений:
SELECT order_id, order_status,
    CASE
        WHEN order_status = 'OPEN' THEN 'Order is in open state'
        WHEN order_status = 'CLOSED' THEN 'Order is closed'
        WHEN order_status = 'CANCELLED' THEN 'Order is in open CANCELLED'
END AS order_summary FROM orders;

# или так
SELECT order_id, order_status,
    CASE order_status
        WHEN 'OPEN' THEN 'Order is in open state'
        WHEN 'CLOSED' THEN 'Order is closed'
        WHEN 'CANCELLED' THEN 'Order is in open CANCELLED'
END AS order_summary FROM orders;


```
4. Чем NULL отличается от 0?

    NULL - это "поле, не содержащее никакого значения" (пустое поле), в то время как 0 - это число, которое, можно отнести например к такому типу данных как INT. Другими словами это разные типы данных.