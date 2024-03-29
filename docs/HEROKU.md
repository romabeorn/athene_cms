# Heroku

## Регистрируемся на платформе heroku.com

https://www.heroku.com/

## Управление приложениями через CLI

Для доступа к приложениям нужно иметь выход к панели управления через Heroku CLI (терминал)

Подробнее об установке вот здесь https://devcenter.heroku.com/articles/heroku-cli

В процессе установки загрузятся heroku, git если его нет.

Переходим в рабочую папку:

    $ git clone https://NICKNAME@bitbucket.org/Almazov/athene-cms.git

Переместитесь в нужную ветку (heroku-platform) и скопируйте содержимое папки athene-cms/athene/
Создайте новую папку, затем поместите в неё скопированные файлы.

Выполните вход в heroku из консоли

    $ heroku login

## Создание нового приложения на heroku

    $ heroku create athene(можно указать свое имя после команды)

## Создание необходимых файлов в корне проекта и добавление зависимостей (там же где находиться project.clj)

- Procfile (запишите в него: web: lein ring server)

- system.properties (запишите в него: java.runtime.version=1.7)

Если в .gitignore нет /target - укажите.

В project.clj впишите минимальную версию lein для запуска проекта

    $ :min-lein-version "2.0.0"

А также укажите зависимость

    $ [ring/ring-servlet "1.2.0-RC1"]

## Инициализация проекта

    $ git init

    $ heroku git:remote -a athene

## Установка БД

Для установки аддонов потребуется ввести данные своей кредитной карты, чтобы верифицировать аккаунт.
Потом можно будет оформлять подписки на дополнения бесплатно (триал версии), либо оплачивать тарифные планы
немного производительнее триальной версии.

Верификация здесь - https://dashboard.heroku.com/account/billing

По окончании перейдите сюда - https://elements.heroku.com/addons/cleardb - Login to Install - Install ClearDB MySQL - Выберите приложение в списке - Continue - Ignite FREE - Provision.
Зайдите в панель управления ClearDB кликнув по аддону.
В таблице My databases кликните по своей базе - Перейдите в Endpoint Information, там содержатся креды для базы (логин, пароль).
Имя БД имеет вид heroku_xxx (У меня heroku_41b7c6e37a83ea7)

Осталось узнать host БД. Для этого вернемся в консоль

    $ heroku config

Скопируйте значение от знака "@" до "/" например us-cdbr-iron-east-03.cleardb.net - Это хост.

## Запуск приложения

Запустите вторую консоль и выполните

    $ heroku logs --app athenecms --tail

Вернитесь в первую консоль

    $ git add .

    $ git commit -m "init"

    $ git push heroku master

Ждите запуска приложения.
После выполните следующее

    $ heroku ps:scale web=1

Откройте приложение по адресу - http://athene.herokuapp.com/
