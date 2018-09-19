

# Описание api

 
Формат общения с API - JSON 

**1. Регистрация пользователя**
POST-запрос на адрес:

    185.159.128.225/registration
Тело запроса:

    {
      "username":"test1@yandex.ru", - логин, почта пользователя
      "password":"Secure177" - пароль
    }
Поле **username** -  максимум 64 символа латиницей, логин обязательно должен быть почтой. Почта проверяется по шаблону: *xxxxxx@server.name*.
Поле **password** - максимум 64 символа латиницей, минимум 8 символов, должен быть хотя бы один заглавный символ, хотя бы один строчный и хотя бы одна цифра.
Ответ:

    {
        "status": 200, - статус 
        "message": "Пользователь успешно зарегистрировался" - сообщение
    }
Список статусов:

    200 - успешно
    405 - такой логин занят 
    400 - неверный запрос 
	
	

 **2. Авторизация  и получение токена**
 POST-запрос на адрес:

    185.159.128.225/login_rest
Тело запроса :

    {
      "username":"test1@yandex.ru", - логин
      "password":"Secure177"- пароль
    }
Поле **username** -  максимум 64 символа латиницей, логин обязательно должен быть почтой. Почта проверяется по шаблону: *xxxxxx@server.name*.
Поле **password** - максимум 64 символа латиницей, минимум 8 символов, должен быть хотя бы один заглавный символ, хотя бы один строчный и хотя бы одна цифра.

Ответ:

    {
        "status": 200, - статус
        "token": "cce8cddec3c27a5366888cf96a156544", - токен
        "token_lt": 14400 - время жизни токена в секундах
    }
Список статусов:

    200 - успешно
    401 - не верный логин/пароль
    400 - неверный запрос
**3. **Получение информации о пользователе****
Получение данных для построения формы "Информация о пользователе".
После регистрации все value  равны null.
GET-запрос на адрес:

    185.159.128.225/user_info/{token}
Где **{token}** - токен полученный при авторизации.
Ответ :

    {
        "form_id": "user_info", - идентификатор формы
        "form_title": "Информация о пользователе", - название формы  
        "fields": [
            {
                "id": "first_name", - идентификатор элемента
                "type": "text", - тип элемента, в данном случае текст
                "light": 50,- макс. длинна значения, 50 знаков
                "label": "Имя", - название элемента
                "value": null - значение элемента
            },
            {
                "id": "patronymic",
                "type": "text",
                "light": 50,
                "label": "Отчество",
                "value": null
            },
            {
                "id": "last_name",
                "type": "text",
                "light": 50,
                "label": "Фамилия",
                "value": null
            },
            {
                "id": "phone",
                "type": "text",
                "light": 50,
                "label": "Номер телефона",
                "value": null
            },
            {
                "id": "sex",
                "type": "enum", - тип элемента с несколькими значениями
                "values": [
                    {
                        "label": "Мужской",
                        "value": "M"
                    },
                    {
                        "label": "Женский",
                        "value": "F"
                    }
                ],
                "label": "Пол",
                "value": null
            },
            {
                "id": "birthday", 
                "type": "date", - тип элемента с датой 
                "format": "YYYY-MM-DD", - формат даты
                "min": "1900-01-01", - дата начала периода
                "max": "2018-08-06", - дата конца периода
                "label": "Дата рождения",
                "value": null
            }
        ]
    }

  
Описание типов:

|Тип| Описание  |
|--|--|
| date | дата
text | текст
enum| поле с несколькими значениями

Описание параметров:

|Параметр |Описание  |
|--|--|
| first_name | Имя, макс. 50 символов |
| patronymic| Отчество, макс. 50 символов |
| last_name| Фамилия, макс. 50 символов |
| phone| Телефон, макс. 50 символов |
| sex| пол, два значения, F - женский, M - мужской |
| phone| Телефон, макс. 50 символов |
| birthday|Дата рождения, период с 1900-01-01 по текущею дату, минус 1 месяц |

Список статусов:

    200 - успешно
    400 - неверный запрос/токен

**4. **Запись информации о пользователе****
POST-запрос на адрес:

    185.159.128.225/user_info/
Тело запроса:

    {    
      "form_id": "user_info", - идентификатор формы
      "token":"94e09d24ac34e6a1cdc6b5e4fe8cd966", - токен полученный при авторизации
      "fields": [
        {
          "id": "first_name",  - идентификатор элемента
          "value": "Александр" - значение элемента
        },
         {
          "id": "last_name",
          "value": "Седов"
        }
      ]
    }
Если идентификатор элемента  - ***id*** не существует для данной формы api вернет ошибку.
Можно передавать от одного до всех значений формы. 

**Задание 1**

Сделать регистрацию пользователя

**Задание 2** 

Сделать авторизацию пользователя

**Задание 3**

Сделать вывод информации о пользователе 

**Задание 4** 

Сделать редактирование информации о пользователе
