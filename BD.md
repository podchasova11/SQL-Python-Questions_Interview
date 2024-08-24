## Вот описание базы данных и SQL-запроса:

# База данных для компании

## Таблица `client`
Содержит информацию о клиентах:
- **id**: уникальный идентификатор клиента (UUID, NOT NULL, PRIMARY KEY)
- **first_name**: имя клиента (TEXT, NOT NULL)
- **last_name**: фамилия клиента (TEXT, NOT NULL)

## Таблица `apartment`
Содержит информацию о квартирах:
- **id**: уникальный идентификатор квартиры (UUID, NOT NULL, PRIMARY KEY)
- **address**: адрес квартиры (TEXT, NOT NULL)
- **rooms**: количество комнат в квартире (INT, NOT NULL)

## Таблица `view`
Содержит информацию о записях на просмотр квартир:
- **id**: уникальный идентификатор записи (UUID, NOT NULL, PRIMARY KEY)
- **apartment_id**: идентификатор квартиры (UUID, NOT NULL, FOREIGN KEY)
- **client_id**: идентификатор клиента (UUID, NOT NULL, FOREIGN KEY)
- **date**: дата просмотра квартиры (TIMESTAMP, NOT NULL)

## SQL-запрос
Запрос для получения списка фамилий клиентов, записанных на просмотр двух и более трёхкомнатных квартир:

```sql
SELECT cl.last_name AS Фамилия
FROM client AS cl
JOIN view v ON cl.id = v.client_id
JOIN apartment ap ON ap.id = v.apartment_id
WHERE ap.rooms >= 3
GROUP BY cl.last_name
HAVING COUNT(DISTINCT(v.apartment_id)) >= 2;
```

Этот запрос:
- Соединяет таблицы `client`, `view` и `apartment`.
- Фильтрует квартиры, где количество комнат три или больше.
- Группирует результаты по фамилиям клиентов.
- Выбирает тех клиентов, которые записаны на просмотр не менее двух таких квартир.


Этот файл может быть использован для документации базы данных и запроса.
