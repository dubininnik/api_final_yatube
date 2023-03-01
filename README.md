# Проект "API для Yatube"

Финальный проект спринта 9 учебного курса "Python Developer" Yandex.Practicum

Представляет собой полноценный API для социальной сети YaTube, реализованный на архитектуре REST API с использользованием библиотеки Django REST Framework.

### Как запустить проект:

Клонировать репозиторий и перейти в него в командной строке:

```
git clone https://github.com/nikdubinin/api_final_yatube.git
```

```
cd api_final_yatube
```

Cоздать и активировать виртуальное окружение:

```
python3 -m venv venv
```

```
source venv/bin/activate
```

Установить зависимости из файла requirements.txt:

```
python3 -m pip install --upgrade pip
```

```
pip install -r requirements.txt
```

Выполнить миграции:

```
python3 manage.py migrate
```

Запустить проект:

```
python3 manage.py runserver
```

## Примеры запросов

* ### Получить JWT-токен
    **Request**
    ```
        POST /api/v1/jwt/create/
        body: {"username": "string", "password": "string"}
    ```
    **Response**
    ```
        {
          "refresh": "string",
          "access": "string",
        }
    ```

* ### Обновить JWT-токен
    **Request**
    ```
        POST /api/v1/jwt/refresh/
        body: {"refresh": "string"}
    ```
    **Response**
    ```
        {
          "access": "string"
        }
    ```

* ### Получение публикаций
    **Request**
    ```
        GET /api/v1/posts/
    ```
    **Response**
    ```
  {
  "count": 123,
  "next": "http://api.example.org/accounts/?offset=400&limit=100",
  "previous": "http://api.example.org/accounts/?offset=200&limit=100",
  "results": [
    {
      "id": 0,
      "author": "string",
      "text": "string",
      "pub_date": "2021-10-14T20:41:29.648Z",
      "image": "string",
      "group": 0
    }
  ]
  }
  ```

* ### Создание публикации
    **Request**
    ```
        POST /api/v1/posts/
        body: {"text": "string", "image": "string or null <binary>", "group": "integer or null"}
    ```
    **Response**
    ```
        {
            "id": 0,
            "author": "string",
            "text": "string",
            "pub_date": "2019-08-24T14:15:22Z"  
            "image": "string",
            "group": 0
        }
    ```

* ### Получение публикации по её id
    **Request**
    ```
        GET /api/v1/posts/{id}/
    ```
    **Response**
    ```
        {
            "id": 0,
            "author": "string",
            "text": "string",
            "pub_date": "2019-08-24T14:15:22Z"  
            "image": "string",
            "group": 0
        }
    ```

* ### Обновление публикации по её id
    **Request**
    ```
        PUT /api/v1/posts/{id}/
        body: {"text": "string", "image": "string or null <binary>", "group": "integer or null"}
    ```
    **Response**
    ```
        {
            "id": 0,
            "author": "string",
            "text": "string",
            "pub_date": "2019-08-24T14:15:22Z"  
            "image": "string",
            "group": 0
        }
   ```

* ### Частичное обновление публикации по её id
    **Request**
    ```
        PATCH /api/v1/posts/{id}/
        body: {"text": "string", "image": "string or null <binary>", "group": "integer or null"}
    ```
    **Response**
    ```
        {
            "id": 0,
            "author": "string",
            "text": "string",
            "pub_date": "2019-08-24T14:15:22Z"  
            "image": "string",
            "group": 0
        }
   ```

* ### Удаление публикации по её id
    **Request**
    ```
        DELETE /api/v1/posts/{id}/
    ```
    **Response**
    ```
        status_code: 204
    ```

* ### Получение списка всех комментариев
    **Request**
    ```
        GET /api/v1/posts/{post_id}/comments/
    ```
    **Response**
    ```
        [
            {
                "id": 0,
                "author": "string",  
                "text": "string",
                "created": "2019-08-24T14:15:22Z"
                "post": 0  
            },
            ...
        ]
    ```

* ### Добавление комментария
    **Request**
    ```
        POST /api/v1/posts/{post_id}/comments/
        body: {"text": "string"}
    ```
    **Response**
    ```
            {
                "id": 0,
                "author": "string",  
                "text": "string",
                "created": "2019-08-24T14:15:22Z"
                "post": 0  
            }
    ```

* ### Получение комментария по его id
    **Request**
    ```
        GET /api/v1/posts/{post_id}/comments/{id}/
    ```
    **Response**
    ```
            {
                "id": 0,
                "author": "string",  
                "text": "string",
                "created": "2019-08-24T14:15:22Z"
                "post": 0  
            }
    ```

* ### Обновление комментария по его id
    **Request**
    ```
        PUT /api/v1/posts/{post_id}/comments/{id}/
        body: {"text: "tring"}
    ```
    **Response**
    ```
            {
                "id": 0,
                "author": "string",  
                "text": "string",
                "created": "2019-08-24T14:15:22Z"
                "post": 0  
            }
    ```

* ### Частичное обновление комментария по его id
    **Request**
    ```
        PATCH /api/v1/posts/{post_id}/comments/{id}/
        body: {"text: "string"}
    ```
    **Response**
    ```
            {
                "id": 0,
                "author": "string",  
                "text": "string",
                "created": "2019-08-24T14:15:22Z"
                "post": 0  
            }
    ```
* ### Удаление комментария по его id
    **Request**
    ```
        DELETE /api/v1/posts/{post_id}/comments/{id}/
    ```
    **Response**
    ```
        status_code: 204
    ```

* ### Получение списка всех подписчиков
    **Request**
    ```
        GET /api/v1/follow/?search={string}
    ```
    **Response**
    ```
        [
            {
                "user": "string",
                "following": "string"
            },
            ...
        ]
    ```

* ### Подписка
    **Request**
    ```
        POST /api/v1/follow/
        body: {"following": "string"}
    ```
    **Response**
    ```
        {
            "user": "string",
            "following": "string"
        }
    ```

* ### Список сообществ
    **Request**
    ```
        GET /api/v1/groups/
    ```
    **Response**
    ```
        [
            {
                "id": "0"
                "title": "string"  
                "slug": "string"
                "description": "string"    
            },
            ...
        ]
    ```

* ### Информация о сообществе
    **Request**
    ```
        GET /api/v1/groups/{id}
    ```
    **Response**
    ```
            {
                "id": "0"
                "title": "string"  
                "slug": "string"
                "description": "string"    
            }
    ```