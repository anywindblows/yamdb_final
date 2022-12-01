[![yamdb_final workflow](https://github.com/anywindblows/yamdb_final/actions/workflows/yamdb_workflow.yaml/badge.svg)](https://github.com/anywindblows/yamdb_final/actions/workflows/yamdb_workflow.yaml)

[![Python](https://img.shields.io/badge/-Python-464646?style=flat-square&logo=Python)](https://www.python.org/)
[![Django](https://img.shields.io/badge/-Django-464646?style=flat-square&logo=Django)](https://www.djangoproject.com/)
[![Django REST Framework](https://img.shields.io/badge/-Django%20REST%20Framework-464646?style=flat-square&logo=Django%20REST%20Framework)](https://www.django-rest-framework.org/)
[![PostgreSQL](https://img.shields.io/badge/-PostgreSQL-464646?style=flat-square&logo=PostgreSQL)](https://www.postgresql.org/)
[![Nginx](https://img.shields.io/badge/-NGINX-464646?style=flat-square&logo=NGINX)](https://nginx.org/ru/)
[![gunicorn](https://img.shields.io/badge/-gunicorn-464646?style=flat-square&logo=gunicorn)](https://gunicorn.org/)
[![docker](https://img.shields.io/badge/-Docker-464646?style=flat-square&logo=docker)](https://www.docker.com/)
[![GitHub%20Actions](https://img.shields.io/badge/-GitHub%20Actions-464646?style=flat-square&logo=GitHub%20actions)](https://github.com/features/actions)
[![Yandex.Cloud](https://img.shields.io/badge/-Yandex.Cloud-464646?style=flat-square&logo=Yandex.Cloud)](https://cloud.yandex.ru/)
___
## **Проект YaMDb:**
- Проект YaMDb собирает отзывы (Review) пользователей на произведения (Titles).
  Произведениям присваивается категория (Category), а так же жанр (Genre).
- Список категорий и жанров устанавливается, и может быть расширен администратором.
- Пользователи оставляют текстовые отзыввы (Review) и ставят оценку в диапазоне от 1 до 10.
- Из пользовательских оценок формируется усреднённая оценка произведения — рейтинг.
- На одно произведение пользователь может оставить только один отзыв.
- Другие пользователи могут оставлять комметарии (Commentary) к отзыву.
___

## Запуск проекта:

1) Клонировать и развернуть репозиторий
```
git clone git@github.com:anywindblows/infra_actions.git
```
2) Установить на удаленном сервере docker и docker-compose
```
sudo apt install docker.io 
```
```
sudo curl -L "https://github.com/docker/compose/releases/download/v2.6.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```
```
sudo chmod +x /usr/local/bin/docker-compose
```
3) Скопируйте файлы docker-compose.yaml и nginx/default.conf из проекта на сервер
4) Добавьте в Secrets GitHub переменные окружения для работы
```
DB_ENGINE=django.db.backends.postgresql
DB_HOST=db
DB_NAME=postgres
DB_PASSWORD=postgres
DB_PORT=5432
DB_USER=postgres

DOCKER_PASSWORD=<DOCKER_PASSWORD>
DOCKER_USERNAME=<DOCKER_USERNAME>

USER=<username для подключения к серверу>
HOST=<IP сервера>
PASSPHRASE=<пароль для сервера, если он установлен>
SSH_KEY=<ваш SSH ключ(cat ~/.ssh/id_rsa)>

TG_CHAT_ID=<ID чата, в который придет сообщение>
TELEGRAM_TOKEN=<токен вашего бота>
```
5) Запушить на Github. После успешного деплоя зайдите на боевой сервер и выполните команды
6) Собрать статические файлы в STATIC_ROOT
```
docker-compose exec web python3 manage.py collectstatic --noinput
```
7) Создать и применить миграции
```
docker-compose exec web python3 manage.py makemigrations
docker-compose exec web python3 manage.py migrate --noinput
```

### Документация проекта
[README.md](https://github.com/anywindblows/api_yamdb/blob/master/README.md)
