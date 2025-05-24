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
| ForeignKey      | поле для создания внешнего ключа      | on_delete=                                      |
|                 | на другую модель (один ко многим)     |                                                 |
| OneToOneField   | создания связи «один к одному»        | on_delete=                                      |
| EmailField      |                                       |                                                 |
