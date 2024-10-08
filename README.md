# Authentication Service

## Описание проекта

Данный проект представляет собой часть сервиса аутентификации, реализующего два REST маршрута для работы с токенами доступа и обновления. Сервис обеспечивает безопасность и защиту токенов, а также уведомляет пользователей о подозрительных действиях.

### REST маршруты

1. **Получение токенов**
   - **Метод:** POST
   - **Маршрут:** /tokens/:id
   - **Параметры:**
     - id (GUID): идентификатор пользователя
   - **Описание:** Возвращает и устаналивает в сесиию пару Access и Refresh токенов для указанного пользователя.
   - **Access токен:** JWT, алгоритм SHA512
   - **Refresh токен:** Хранится в базе как bcrypt хеш.

2. **Refresh операция**
   - **Метод:** POST
   - **Маршрут:** /tokens/refresh
   - **Описание:** Обновляет Access токен и Refresh токен, если Refresh токен действителен.
   - В случае изменения IP адреса клиента отправляется предупреждение на электронную почту пользователя (в проекте используются моковые данные).


## Дополнительные REST маршруты

1. **Регистрация пользователя**
   - **Метод:** POST
   - **Маршрут:** /auth/sign-up
   - **Body**
     ```json { "email": "ur_email", "password": "ur_password" }```
   - **Описание:** Регестрирует пользователя в системе, записывает его логин, пароль и ip адрес.


2. **Аунтификация пользователя**
   - **Метод:** POST
   - **Маршрут:** /auth/sign-in
   - **Body**
     ```json { "email": "ur_email", "password": "ur_password" }```
   - **Описание:** Если пользователя с ввел валидные данные, выдается Access и Refresh токены.


3. **Функция для для проверки работы токенов**
   - **Метод:** POST
   - **Маршрут:** /test
   - **Описание:** Доступ к данной функции доступен только авторизированным пользователям с валидным access токеном. В качестве ответа функция возвращает Json с сообщением, что юзер получил доступ.


## Запуск

**В проекте используется .env файл!** Не забудьте создать его с полями:
- DB_PASSWORD:"-"
- SIGNING_KEY:"-"
- EMAIL_PASSWORD:"-"

Используя Makefile, который есть в проекте:
- make compile - обновляет go.mod и go.sum
- make run - запускает апи


