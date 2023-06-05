![MySQL](/Sem4/Mysql.png)

```sql
# создание базы данных
CREATE DATABASE hw4;

# выбор бд для работы
USE hw4;

# создание сущности (таблица AUTO)
CREATE TABLE AUTO 
(       
	REGNUM VARCHAR(10) PRIMARY KEY, 
	MARK VARCHAR(10), 
	COLOR VARCHAR(15),
	RELEASEDT DATE, 
	PHONENUM VARCHAR(15)
);

```
![Таблица AUTO](/Sem4/AUTO.png)

1. Вывести на экран сколько машин каждого цвета для машин марок BMW и LADA

```sql
SELECT mark, color, COUNT(color) FROM AUTO
WHERE (mark = 'BMW' OR mark = 'LADA')
GROUP BY  mark, color;
```
2. Вывести на экран марку авто и количество AUTO не этой марки


3. Даны 2 таблицы, созданные следующим образом:
```sql
create table test_a (id number, data varchar2(1));
create table test_b (id number);
insert into test_a(id, data) values
(10, 'A'),
(20, 'A'),
(30, 'F'),
(40, 'D'),
(50, 'C');
insert into test_b(id) values
(10),
(30),
(50);
```

Напишите запрос, который вернет строки из таблицы test_a, id которых нет в таблице test_b, НЕ используя ключевого слова NOT.

```sql
SELECT a.* FROM test_a A 
LEFT JOIN test_b B 
ON a.id = b.id # условие объединения
WHERE b.id IS NULL;
```
---
Подготовил студент Geek Brains - **Ивлев Павел**.