Вы должны были выполнить следующие задания:

Создать проект Django.
Добавить в него 3 статические странички. На одной из них текст полностью оформлен курсивом.
На одной из страниц контент повторяется 2 раза без изменения content (два раза прописано {{ flatpage.content }}).
Одна из страниц на сайте доступна только админу (только вошедшему пользователю).
На одной из страниц изменены шрифты и размеры текста.
Сайт представляет собой оформленный Bootstrap-шаблон со встроенными пользовательскими данными.

---------------Шаги---------------------------
Создать виртуальное локальное окружение: python -m venv venv
и активировать его: venv\scripts\activate
Создание проекта в командной строке: django-admin startproject django_project
перейти в директорию: cd django_project
и запустить сервер: python manage.py runserver
остановить сервер командой: ctrl + C
Запустить миграцию файлов: python manage.py migrate
создать администратора: python manage.py createsuperuser

подключить странички:
INSTALLED_APPS = [...
# added pages
    'django.contrib.sites',
    'django.contrib.flatpages',
]
SITE_ID=1

файл urls.py:

from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('pages/', include('django.contrib.flatpages.urls')),
]

файл setting:
MIDDLEWARE = [
....
 
    'django.contrib.flatpages.middleware.FlatpageFallbackMiddleware, 
]
Так как добавлены новые приложения, нам необходимо опять применить миграции, чтобы они смогли использовать 
базу данных (не забываем, что остановить работу текущего проекта можно комбинацией клавиш Ctrl + C).
python manage.py migrate

В директории с файлом manage.py нужно создать файл по следующему пути: templates/flatpages/default.html.

Если не находит путь в setting добавить
import os
TEMPLATES = [...
'DIRS': [os.path.join(BASE_DIR, 'templates')],

