# Косьмин Павел, 153501
## Используемая технология
Postgre sql
## Предметная область 
Книжный магазин
## Функциональные требования
* Пользователь может зайти как клиент или как супер пользователь.
* Супер пользователь может добавлять новые книги в продажу
* Супер пользователь может добавлять в новые книги автора, издательство, жанры
* Супер пользователь может удалять новые книги из продажи
* Супер пользователь может добавлять новые жанры
* Супер пользователь может удалять жанры
* Супер пользователь может добавлять новых авторов
* Супер пользователь может удалять авторов
* Супер пользователь может добавлять новые издательства
* Супер пользователь может удалять издательства
* Супер пользователь может добавлять пункт выдачи
* Супер пользователь может удалять пункт выдачи
* Супер пользователь может просматривать отзывы
* Клиент может просматривать книги на продажу
* Клиент может покупать книги
* Клиент может добавлять отзывы
* Клиент может удалять отзывы
* Клиент может просматривать отзывы
* Клиент может оформлять заказ
## Список таблиц
### Пользователи
* Описание
  + Хранит данные для входа студента или суперпоользователя
* Поля
  + id (Primary Key, INT, Auto-increment, NN) - уникальный идентификатор пользователя
  + username (VARCHAR(50), NN) - логин
  + password (VARCHAR(50), NN) - пароль
  + is_superuser (BOOL, NN) - является ли пользователь супер пользователем
* Связи
  + один к нулю или одному с таблицей Студенты
### Клиенты
* Описание
  + Хранит данные о клиентах
* Поля
  + id (Primary Key, INT, Auto-increment, NN) - уникальный идентификатор клиента
  + user_id (Foreign Key, INT, NN) - уникальный идентификатор клиента
  + first_name (VARCHAR(50), NN) - имя клиента
  + last_name (VARCHAR(50), NN) - фамилия клиента
  + email (VARCHAR(50), NN) - электронная почта клиента
  + phone_number (VARCHAR(50), NN) - номер телефона клиента
* Связи
  + один к одному связь с таблицей юзер(через поле user_id)
  + один ко многим связь с таблицей заказы
### Заказ
* Описание
  + Хранит заказы
* Поля
  + id (Primary Key, INT, Auto-increment, NN) - уникальный идентификатор заказа
  + date (DATE, NN) - дата заказа
  + status (VARCHAR(50), NN) - статус
  + client_id (Foreign Key, INT, NN) - уникальный идентификатор клиента
  + pick_up_point_id (Foreign Key, INT, NN) - уникальный идентификатор пункта выдачи
* Связи
  + многие к одному связь с таблицей клиенты(через поле client_id)
  + многие к одному связь с пунктом выдачи(через поле pick_up_point_id)
  + один ко многим связь с книга заказов
### Книга заказ
* Описание
  + Хранит заказы на конкретные книги
* Поля
  + id (Primary Key, INT, Auto-increment, NN) - уникальный идентификатор книги заказов
  + book_id (Foreign Key, INT, NN) - уникальный идентификатор книги
  + order_id (Foreign Key, INT, NN) - уникальный идентификатор заказа
  + quantity (INT, NN) - количество книг
* Связи
  + многие к одному связь с таблицей заказы(через поле book_id)
  + один ко многим связь с таблицей книги(через поле order_id)
### Книги
* Описание
  + Хранит книги
* Поля
  + id (Primary Key, INT, Auto-increment, NN) - уникальный идентификатор книги
  + title (VARCHAR(50), NN) - название
  + author_id (Foreign Key, INT, NN) - уникальный идентификатор автора
  + publishing_house_id (Foreign Key, INT, NN) - уникальный идентификатор издательства
  + creation_year (VARCHAR(50), NN) - год создания
  + isbn (INT, NN) - isbn номер
  + price (VARCHAR(50), NN) - цена
  + quantity (INT, NN) - количество книг
* Связи
  + один ко многим связь с таблицей жанры
  + один ко многим с таблицами отзывы о книге
  + один ко многим с таблицей книга заказ
  + многие ко одному с таблицей автор(через поле author_id)
  + многие к одному с таблицей издательство(через поле publishing_house_id)
### Жанры
* Описание
  + Хранит жанры книг
* Поля
  + id (Primary Key, INT, Auto-increment, NN) - уникальный идентификатор жанров
  + title (VARCHAR(50), NN) - название жанра
* Связи
  + один ко многим связь с книга жанрами
### Книга жанры
* Описание
  + Хранит конкретные жанры
* Поля
  + id (Primary Key, INT, Auto-increment, NN) - уникальный идентификатор жанров
  + genre_id (Foreign Key, INT, NN) - уникальный идентификатор жанра
  + book_id (Foreign Key, INT, NN) - уникальный идентификатор книги
* Связи
  + многие к одному связь с книгами(через поле book_id)
  + многие к одному связь с жанрами(через поле genre_id)
### Авторы
* Описание
  + Хранит информацию о авторах
* Поля
  + id (Primary Key, INT, Auto-increment, NN) - уникальный идентификатор авторов
  + first_name (VARCHAR(50), NN) - имя автора
  + last_name (VARCHAR(50), NN) - фамилия автора
  + birthday_date (DATE, NN) - дата рождения автора
  + biography (VARCHAR(50), NN) - биография автора
* Связи
  + один ко одному связь с книгами
### Издательства
* Описание
  + Хранит информацию о издательствах
* Поля
  + id (Primary Key, INT, Auto-increment, NN) - уникальный идентификатор издательств
  + name (VARCHAR(50), NN) - название издательства
  + address (VARCHAR(50), NN) - адрес
  + phone_number (VARCHAR(50), NN) - номер телефона
  + email (VARCHAR(50), NN) - электронная почта
* Связи
  + один ко одному связь с таблицей книг
### Отзывы
* Описание
  + Хранит информацию о отзывах
* Поля
  + id (Primary Key, INT, Auto-increment) - уникальный идентификатор отзывов
  + review_text (VARCHAR(500), NN) - текст отзыва
  + add_date (DATE, NN) - дата добавления
  + book_id (Foreign Key, INT, NN) - уникальный идентификатор книги
* Связи
  + многие к одному связь с книгой(через поле book_id)
### Пункты выдачи
* Описание
  + Хранит пункты выдачи
* Поля
  + id (Primary Key, INT, Auto-increment, NN) - уникальный идентификатор пункта выдачи
  + street (VARCHAR(50), NN) - название улицы
  + house_num (INT, NN) - номер дома
  + housing (INT) - корпус
* Связи
  + один к одному связь с пунктами выдачи