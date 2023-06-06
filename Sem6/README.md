![MySQL](/Sem4/Mysql.png)

Задание №1
Создайте функцию, которая принимает кол-во сек и форматирует их в кол-во дней, часов, минут и секунд. 
Пример: 123456 ->'1 days 10 hours 17 minutes 36 seconds'

```sql
DROP FUNCTION format;
DELIMITER //
CREATE FUNCTION format (num INT)
RETURNS VARCHAR(100)
DETERMINISTIC
BEGIN
    DECLARE days CHAR(3);
    DECLARE hours, minutes, seconds CHAR(2);
    DECLARE ost, ost1 INT;
    DECLARE result VARCHAR(100);

    SET days = CAST(num DIV (60*60*24) AS CHAR(3)) -- количество дней;
    SET ost = num % (60*60*24) # остаток

    SET hours = CAST(ost DIV (60*60) AS CHAR(2)) -- количество часов
    SET ost1 = ost % (60*60) # остаток1

    SET minutes = CAST(ost1 DIV (60) AS CHAR(2)) -- количество минут

    SET seconds = CAST(ost1 % (60) AS CHAR(2)) -- количество секунд

    SET result = CONCAT(num, " -> ", days, " days ", hours, ' hours ', minutes, ' minutes ', seconds, ' seconds')
    RETURN result;
END //
DELIMITER ;

SELECT format(123456); -- запуск функции
```

Задача №2
Выведите только четные числа от 1 до 10. Пример: 2,4,6,8,10

```sql
DROP FUNCTION even_numbers;

DELIMITER //
CREATE FUNCTION even_numbers ()
RETURNS VARCHAR(100)
DETERMINISTIC
BEGIN
DECLARE i INT DEFAULT 1;
DECLARE result VARCHAR(100) DEFAULT "";
	WHILE i <= 10 DO
		IF (i % 2 = 0) THEN
			SET result = concat(result, " ", i);
			SET i = i + 2;
		ELSE
			SET i = i + 1;
        END IF;
	END WHILE;
RETURN result;
END //
DELIMITER ;

SELECT even_numbers(); -- запуск функции
```
---
Подготовил студент Geek Brains - **Ивлев Павел**.