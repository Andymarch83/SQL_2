# Урок 2. SQL – создание объектов, изменение данных, логические операторы

#### ЛЕКЦИЯ: https://pollen-attempt-4ac.notion.site/SQL-2-d8ccb2206c9941b6acd594d06689abb7 ; https://gbcdn.mrgcdn.ru/uploads/record/245972/attachment/92748e89925a323a0871d89e356920b5.mp4


#### https://gbcdn.mrgcdn.ru/uploads/asset/4490288/attachment/edf6e20c0d2491463d17e6f852c5c835.pdf
#### https://gbcdn.mrgcdn.ru/uploads/asset/4490294/attachment/a0a530ba8def537e5bb925127fcea978.pdf

План урока:
- Типы данных, значения NULL, create table, PK, FK, index
- Комментарии
- Арифметических операции
- Логические операторы (and, or, between, not, in)
- Приоритет выполнения операторов, порядок выполнения запроса
- Оператор CASE, IF
- Запросы изменения данных (insert, update, delete)


#### ВЕБИНАР: https://gbcdn.mrgcdn.ru/uploads/record/289484/attachment/6fedcea2168794a7c934604cab78fecc.mp4
#### https://gbcdn.mrgcdn.ru/uploads/asset/5650615/attachment/3bfac31a30a4e5f31eb5f7e03b745f01.pdf

План урока:
- Работа с таблицами: создание и заполнение
- Манипуляции с таблицами
- Использование оператора CASE и функции IF()


#### 1. Создать таблицу sales с тремя столбцами: id, order_date (дата заказа) и count_product (количество продуктов в заказе). Затем заполнить эту таблицу данными, включая информацию о дате заказа и количестве продуктов в каждом заказе. Названия столбцов: order_date, count_product. Заполните ее данными.

-- Создание таблицы "sales"

DROP TABLE IF EXISTS {schema_name}.sales;

CREATE TABLE {schema_name}.sales (

 id SERIAL PRIMARY KEY,
 
 order_date DATE,
 
 count_product INT
 
);

-- Заполнение данными таблицы sales

INSERT INTO {schema_name}.sales (order_date, count_product)

VALUES 

('2022-01-01', 156),

('2022-01-02', 180),

('2022-01-03', 21),

('2022-01-04', 124),

('2022-01-05', 341);


#### 2. Для данных таблицы sales укажите тип заказа в зависимости от кол-ва :

меньше 100 - Маленький заказ,

от 100 до 300 - Средний заказ,

больше 300 - Большой заказ.

Выведите таблицу с названиями столбцов Номер заказа, Количество продукта, Тип

SELECT

  id AS "Номер заказа",
  
  count_product AS "Количество продукта",
  
  CASE
  
    WHEN count_product < 100 THEN 'Маленький заказ'
    
    WHEN count_product BETWEEN 100 AND 300 THEN 'Средний заказ'
    
    WHEN count_product > 300 THEN 'Большой заказ'
    
    ELSE 'Не определено'
    
  END AS "Тип"
  
FROM sales;

#### 3. Используя операторы языка SQL, создайте таблицу orders, заполните ее значениями. Названия столбцов: employee_id, amount, order_status.

-- Создание таблицы "orders"

DROP TABLE IF EXISTS {schema_name}.orders;

CREATE TABLE {schema_name}.orders (

 id SERIAL PRIMARY KEY, 
 
 employee_id VARCHAR(10),
 
 amount NUMERIC(5,2),
 
 order_status VARCHAR(10) CHECK (order_status IN ('OPEN', 'CLOSED', 'CANCELLED'))
 
);

-- Заполнение значениями таблицы "orders"

INSERT INTO {schema_name}.orders (employee_id, amount, order_status)

VALUES

('e03', '15.00', 'OPEN'),

('e01', '25.50', 'OPEN'),

('e05', '100.70', 'CLOSED'),

('e02', '22.18', 'OPEN'),

('e04', '9.50', 'CANCELLED'); 


#### 4. Выбрать данные из таблицыorders и вывести столбцы id, employee_id, amount, и order_status с дополнительным столбцом full_order_status, который содержит описание статуса заказа на основе значения столбца 'order_status'.

SELECT id, employee_id, amount, order_status,

    CASE order_status 
    
        WHEN 'OPEN' THEN 'Order is in open state'
        
        WHEN 'CLOSED' THEN 'Order is closed'
        
        WHEN 'CANCELLED' THEN 'Order is cancelled'
        
        ELSE 'Not mentioned'
        
    END AS full_order_status 
    
FROM orders;







