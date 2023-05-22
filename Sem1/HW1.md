1. Создайте таблицу с мобильными телефонами, используя графический интерфейс. Id, ProductName, Manufacturer, ProductCount, Price. Заполните БД данными.

```sql
CREATE SCHEMA `phonedb` ;
INSERT INTO `phonedb`.`phonedb` (`Id`, `ProductName`, `Manufacturer`, `ProductCount`, `Price`) VALUES ('1', 'iPhone 4', 'Apple', '20', '7000');
INSERT INTO `phonedb`.`phonedb` (`Id`, `ProductName`, `Manufacturer`, `ProductCount`, `Price`) VALUES ('2', 'iPhone 5C', 'Apple', '100', '10000');
INSERT INTO `phonedb`.`phonedb` (`Id`, `ProductName`, `Manufacturer`, `ProductCount`, `Price`) VALUES ('4', 'iPhone 13 mini', 'Apple', '50', '40000');
INSERT INTO `phonedb`.`phonedb` (`Id`, `ProductName`, `Manufacturer`, `ProductCount`, `Price`) VALUES ('5', 'Galaxy S', 'Sumsung', '20', '45000');
INSERT INTO `phonedb`.`phonedb` (`Id`, `ProductName`, `Manufacturer`, `ProductCount`, `Price`) VALUES ('6', 'Galaxy M', 'Sumsung', '90', '47000');
INSERT INTO `phonedb`.`phonedb` (`Id`, `ProductName`, `Manufacturer`, `ProductCount`, `Price`) VALUES ('7', 'Galaxy Note 2', 'Sumsung', '80', '50000');
INSERT INTO `phonedb`.`phonedb` (`Id`, `ProductName`, `Manufacturer`, `ProductCount`, `Price`) VALUES ('8', 'Mi 5 Pro', 'Xiaomi', '101', '24000');
```
---
2. Выведите название, производителя и цену для товаров, количество которых превышает 2 (я поставил 70)

```sql
SELECT ProductName, Manufacturer, Price FROM phonedb.phonedb WHERE ProductCount > 70;
```

---
3. Выведите весь ассортимент товаров марки “Sumsung”
```sql
SELECT * FROM phonedb.phonedb WHERE Manufacturer = 'Sumsung';
```
4. С помощью регулярных выражений найти:
 - Товары, в наименовании которых есть упоминание "Iphone"
 ```sql
 SELECT * FROM phonedb.phonedb WHERE ProductName LIKE 'iPhone%';
 ```
 - Товары, в наименовании которых есть упоминание "Samsung"
 ```sql
 SELECT * FROM phonedb.phonedb WHERE Manufacturer LIKE 'Sumsung%';
 ```
 - Товары, в наименовании которых есть ЦИФРЫ:
 ```sql
 SELECT * FROM phonedb.phonedb WHERE ProductName REGEXP '[0-9]';
 ```
 - Товары, в наименовании которых есть ЦИФРА "8" (а у меня 4):
 ```sql
  SELECT * FROM phonedb.phonedb WHERE ProductName REGEXP '[4]'
  ```