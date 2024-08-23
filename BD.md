Описание и схема базы данных:
Таблица client, которая содержит информацию о клиентах компании. Она содержит поля:
id – уникальный идентификатор клиента;
first_name – имя клиента;
last_name – фамилия клиента.
Таблица apartment, которая содержит информацию о продаваемых квартирах. Она содержит поля:
id – уникальный идентификатор квартиры;
address – адрес квартиры;
rooms – количество комнат в квартире.
Таблица view, которая содержит информацию о записи на просмотр квартир клиентами. Она содержит поля:
id – уникальный идентификатор записи;
apartment_id – идентификатор квартиры;
client_id – идентификатор клиента, записанного на просмотр;
date – дата просмотра квартиры.
Таблица client
+-----------+-----------+-----------+
|    id     | first_name| last_name |
+-----------+-----------+-----------+
| UUID NOT  | TEXT NOT  | TEXT NOT  |
| NULL PK   | NULL      | NULL      |
+-----------+-----------+-----------+

Таблица apartment
+-----------+-----------+-----------+
|    id     |  address  |   rooms   |
+-----------+-----------+-----------+
| UUID NOT  | TEXT NOT  | INT NOT   |
| NULL PK   | NULL      | NULL      |
+-----------+-----------+-----------+

Таблица view
+-----------+-------------+-----------+---------------------+
|    id     | apartment_id| client_id |        date         |
+-----------+-------------+-----------+---------------------+
| UUID NOT  | UUID NOT    | UUID NOT  | TIMESTAMP NOT NULL  |
| NULL PK   | NULL FK     | NULL FK   |                     |
+-----------+-------------+-----------+---------------------+



Для PostgreSQL
https://metanit.com/sql/postgresql/2.3.php

https://sqliteonline.com/

SQL-запрос для получения списка фамилий клиентов, записанных на просмотр двух и более трёхкомнатных квартир.

При вставке значений укажите еще больше своих значений, чтобы получить результат.

CREATE TABLE client (
    id serial NOT NULL PRIMARY KEY,
    first_name varchar NOT NULL,
    last_name varchar NOT NULL
);

CREATE TABLE apartment (
    id serial NOT NULL PRIMARY KEY,
    address varchar NOT NULL,
    rooms INT NOT NULL
);

CREATE TABLE view (
    id serial NOT NULL PRIMARY KEY,
    apartment_id int NOT NULL,
    client_id int NOT NULL,
    date TIMESTAMP NOT NULL
);

-- Вставка данных в таблицу client
INSERT INTO client (first_name, last_name) VALUES
('John', 'Doe'),
('Jane', 'Smith');

-- Вставка данных в таблицу apartment
INSERT INTO apartment (address, rooms) VALUES
('123 Main St', 2),
('456 Elm St', 3),
('789 Oak St', 4);

-- Вставка данных в таблицу view
INSERT INTO view (apartment_id, client_id, date) VALUES
(2, 1, '2023-01-01 10:00:00'),
(1, 2, '2023-01-02 11:00:00'),
(3, 3, '2023-01-03 12:00:00');

SELECT * FROM client
SELECT * FROM apartment
SELECT * FROM view

— Решение 

SELECT cl.last_name as Фамилия FROM client as cl
join view v ON cl.id = v.client_id
JOIN apartment ap ON ap.id = v.apartment_id
WHERE ap.rooms = 3
GROUP by cl.last_name
HAVING COUNT(DISTINCT(v.apartment_id)) >= 2


Этот запрос делает следующее:
Соединяет таблицы client, view и apartment.
Фильтрует квартиры, где количество комнат три или больше.
Группирует результаты по фамилиям клиентов.
Отбирает те группы, в которых клиент записался на просмотр не менее двух таких квартир.
