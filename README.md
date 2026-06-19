# API Yatube

REST API для социальной сети Yatube, где пользователи могут публиковать посты, оставлять комментарии, объединяться в сообщества и подписываться друг на друга.

## Технологии

- Python 3.9
- Django 3.2
- Django REST Framework 3.12
- SimpleJWT
- SQLite

## Установка

1. Клонируйте репозиторий:
```bash
git clone https://github.com/vanda3000/api-final-yatube-ad.git
cd api-final-yatube-ad
```

2. Создайте и активируйте виртуальное окружение:
```bash
python -m venv venv
source venv/bin/activate  # Linux/Mac
venv\Scripts\activate     # Windows
```

3. Установите зависимости:
```bash
pip install -r requirements.txt
```

4. Выполните миграции:
```bash
cd yatube_api
python manage.py migrate
```

5. Запустите сервер:
```bash
python manage.py runserver
```

Документация API доступна по адресу: http://127.0.0.1:8000/redoc/

## Аутентификация

API использует JWT-токены. Для получения токена отправьте POST-запрос:

```
POST /api/v1/jwt/create/
Content-Type: application/json

{
  "username": "your_username",
  "password": "your_password"
}
```

Полученный `access` токен передавайте в заголовке:
```
Authorization: Bearer <ваш_токен>
```

## Примеры запросов

### Получить список постов
```
GET /api/v1/posts/
```

### Создать пост
```
POST /api/v1/posts/
Authorization: Bearer <токен>

{
  "text": "Текст публикации",
  "group": 1
}
```

### Добавить комментарий
```
POST /api/v1/posts/1/comments/
Authorization: Bearer <токен>

{
  "text": "Текст комментария"
}
```

### Подписаться на пользователя
```
POST /api/v1/follow/
Authorization: Bearer <токен>

{
  "following": "username"
}
```

### Получить свои подписки
```
GET /api/v1/follow/
Authorization: Bearer <токен>
```

### Поиск по подпискам
```
GET /api/v1/follow/?search=username
Authorization: Bearer <токен>
```

## Права доступа

- Неаутентифицированные пользователи могут только читать посты, комментарии и список сообществ.
- Аутентифицированные пользователи могут создавать посты и комментарии, а также редактировать и удалять **свой** контент.
- Эндпоинт `/api/v1/follow/` доступен только аутентифицированным пользователям.
