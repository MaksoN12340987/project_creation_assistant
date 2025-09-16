# CONFIG PROJECT

Шаги, необходимые для установки виртуального окружения:

#### Создайте виртуальное окружение:
```
python3 -m venv venv
```

#### Активируйте виртуальное окружение:
Для macOS и Linux:
```
source venv/bin/activate
```

Windows:
```
venv\Scripts\activate
```

#### Устанавливаем Django
После создания виртуального окружения мы должны установить пакет для работы с Django. Пакет называется 
django и устанавливается следующей командой:
```
pip install django
```

Не забывайте сохранять список зависимостей, если используете pip и venv:
```
pip freeze > requirements.txt
```


1. Инициализация проекта внутри текущей директории
Для этого используется следующая команда:
```
django-admin startproject config .
```


#### Для создания нового приложения в проекте Django используйте команду:
```
python manage.py startapp app_name
```



#### Запуск сервера разработки
Django предоставляет встроенный сервер разработки, который позволяет вам тестировать ваше приложение локально. Запуск сервера разработки происходит с помощью команды 
runserver:
```
python manage.py runserver
```


#### Миграции — это механизм, позволяющий управлять изменениями в структуре базы данных. Каждый раз, когда вы вносите изменения в модели, вам нужно создать и применить миграции.

Управляет зависимостями БД - migrations
Управляет данными - admin.py
Конфиг приложения - apps.py
Модели данных - models.py
Тестирование - tests.py
Контроллеры - views.py


#### Не забудте создать urls.py в проекте и связать пути через "include"
```
from django.urls import path
from . import views
from catalog.apps import AppConfig


app_name = AppConfig.name

urlpatterns = [
    path('home/', views.about, name='home'),
    path(f'{AppConfig.name}/', views.contact, name=f'{AppConfig.name}')
]
```



#### Добавить в config/settings.py приложение в константе INSTALLED_APPS
И также добавить:
```
STATIC_URL = '/static/'
```

Настройки для 
```

```

Настройки для подтягивания из .env
```
SECRET_KEY = os.getenv("SECRET_KEY")
DEBUG = True if os.getenv("DEBUG") == "True" else False
EMAIL_BACKEND = os.getenv("EMAIL_BACKEND")
EMAIL_HOST = os.getenv("EMAIL_HOST", default="smtp.yandex.ru")
EMAIL_PORT = os.getenv("EMAIL_PORT", default="465")
EMAIL_USE_TLS = True if os.getenv("EMAIL_USE_TLS") == "True" else False
EMAIL_USE_SSL = True if os.getenv("EMAIL_USE_SSL") == "True" else False
EMAIL_HOST_USER = os.getenv("EMAIL_HOST_USER", default="gorscheneow2018@yandex.ru")
EMAIL_HOST_PASSWORD = os.getenv("EMAIL_HOST_PASSWORD")
DEFAULT_FROM_EMAIL = os.getenv(
    "DEFAULT_FROM_EMAIL", default="gorscheneow2018@yandex.ru"
)
```

```
MEDIA_URL = '/media/'

MEDIA_ROOT = BASE_DIR / 'media'
```
```
LANGUAGE_CODE = "en-us"

TIME_ZONE = "UTC"

USE_L10N = True

USE_I18N = True

USE_TZ = True
```

### Data type
| TYPE            | DESCRIPNION                           | PAREMRTRS                                       |
|                 |                                       | unique - поле должно быть уникальным            |
|                 |                                       | help_text - текст подсказки для поля в админке  |
| CharField       | поле для хранения строк               | max_length=150                                  |
|                 |                                       | verbose_name='Имя' - читаемое имя поля          |
| IntegerField    | хранения целых чисел                  |                                                 |
| BooleanField    | хранения булевых значений             | default=True                                    |
| TextField       | хранения больших текстов              | null=True - может ли поле быть NULL             |
|                 |                                       | blank=True - может ли поле быть пустым в формах |
| DateTimeField   | хранения даты и времени               |                                                 |
| ImageField      | информация о загруженных изображениях |                                                 |
| ForeignKey      | поле для создания внешнего ключа      | on_delete                                       |
|                 | на другую модель (один ко многим)     |                                                 |
| OneToOneField   | создания связи «один к одному»        |                                                 |
| EmailField      |                                       |                                                 |

```
    first_name = models.CharField(max_length=150, verbose_name='Имя')
    last_name = models.CharField(max_length=150, verbose_name='Фамилия')
    
    age = models.IntegerField( help_text="Введите возвраст")
    is_activ = models.BooleanField(default=True)
    descripyion = models.TextField(null=True, blank=True)\
        # null — определяет, может ли поле принимать значение NULL
        # blank — определяет, может ли поле быть пустым в формах. Полезно для валидации данных.
    create_at = models.DateTimeField(auto_now_add=True)
    
    image = models.ImageField(upload_to='photos/', verbose_name='Фотография')
    
    # Зависимость данных один ко многим
    group = models.ForeignKey(Group, on_delete=models.CASCADE)
    
    # Один к одному
    profils = models.OneToOneField(Profile, on_delete=models.CASCADE)
    
    # Многие ко многим
    tags = models.ManyToManyField(Tag)
    
    STATUS_CHOICES = [
        ('draft', 'Draft')
        ('published', 'Published')
    ]
    status = models.CharField()
```


## Migrations

#### Create file migrations

```
python manage.py makemigrations
```
=> 0001_initial.py

#### Применить миграцию
```
python manage.py migrate
```

#### Откатить миграцию
```
python manage.py migrate app_name 0001
```

#### Вернуть в исходное состояние, отменить все миграции
```
python manage.py migrate app_name zero
```


## Django shell
#### IPython
Это улучшенная интерактивная оболочка для Python, которая предоставляет более удобный интерфейс, автодополнение, синтаксическую подсветку и другие полезные функции.

Чтобы использовать IPython в Django shell, установите IPython:
```
poetry add ipython
```
После установки запустите Django shell с IPython:
```
python manage.py shell -i ipython
```

## Чтение данных
```
students = Student.objects.all()
```


## Заполнение данными
#### Создание json файла для простого заполнения данными БД
```
python -Xutf8 manage.py dumpdata [app_label].[model_name] --output file.json --indent 4
```


# Кастомные пользователи
Настройки в setings
```
AUTH_USER_MODEL = "users.BaseUser"
LOGIN_REDIRECT_URL = "catalog:home"
LOGOUT_REDIRECT_URL = "users:login"
```

```
LOGIN_URL = "users:login"
```


# Получение и отправка сообщений по почте
Настройки в setings
```
EMAIL_BACKEND = os.getenv("EMAIL_BACKEND")
EMAIL_HOST = os.getenv("EMAIL_HOST", default="smtp.yandex.ru")
EMAIL_PORT = os.getenv("EMAIL_PORT", default="465")
EMAIL_USE_TLS = True if os.getenv("EMAIL_USE_TLS") == "True" else False
EMAIL_USE_SSL = True if os.getenv("EMAIL_USE_SSL") == "True" else False
EMAIL_HOST_USER = os.getenv("EMAIL_HOST_USER", default="gorscheneow2018@yandex.ru")
EMAIL_HOST_PASSWORD = os.getenv("EMAIL_HOST_PASSWORD")
DEFAULT_FROM_EMAIL = os.getenv(
    "DEFAULT_FROM_EMAIL", default="gorscheneow2018@yandex.ru"
)
```


# Настройка базы данных
Настройки в setings
```
DATABASES = {
    "default": {
        "ENGINE": "django.db.backends.postgresql_psycopg2",
        "PORT": os.getenv("DATABASE_PORT", default="5432"),
        "NAME": os.getenv("DATABASE_NAME", default="postgres"),
        "USER": os.getenv("DATABASE_USER", default="postgres"),
        "HOST": os.getenv("DATABASE_HOST", default="localhost"),
        "PASSWORD": os.getenv("DATABASE_PASSWORD"),
    }
}
```


# Настройка кеширования
Настройки в setings
```
CACHES = {
    "default": {
        "BACKEND": os.getenv(
            "BACKEND", default="django.core.cache.backends.redis.RedisCache"
        ),
        "LOCATION": os.getenv("LOCATION", default="redis://127.0.0.1:6379/1"),
    }
}
```


# Пример .env
SECRET_KEY="django-insecure-kw&o6na0bg6=!=deyi%q$+#9my14*wr45h#v8f_cifxje23*tf"

DEBUG=True

DATABASE_PORT=5432
DATABASE_NAME=postgres
DATABASE_USER=postgres
DATABASE_HOST=localhost
DATABASE_PASSWORD=pi

WORDS_PROHIBITED=казино.криптовалюта.крипта.биржа.дешево.бесплатно.обман.полиция.радар

EMAIL_BACKEND=django.core.mail.backends.smtp.EmailBackend
EMAIL_HOST=smtp.yandex.ru
EMAIL_PORT=465
EMAIL_USE_TLS=False
EMAIL_USE_SSL=True
EMAIL_HOST_USER=gorscheneow2018@yandex.ru
EMAIL_HOST_PASSWORD=lhubxvbwpplacfwz
