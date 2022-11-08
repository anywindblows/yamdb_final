[![yamdb_final workflow](https://github.com/anywindblows/yamdb_final/actions/workflows/yamdb_workflow.yaml/badge.svg)](https://github.com/anywindblows/yamdb_final/actions/workflows/yamdb_workflow.yaml)


## IP: 178.154.203.237

## **Проект YaMDb:**

- Проект YaMDb собирает отзывы (Review) пользователей на произведения (Titles).
  Произведениям присваивается категория (Category), а так же жанр (Genre).
- Список категорий и жанров устанавливается, и может быть расширен администратором.
- Пользователи оставляют текстовые отзыввы (Review) и ставят оценку в диапазоне от 1 до 10.
- Из пользовательских оценок формируется усреднённая оценка произведения — рейтинг.
- На одно произведение пользователь может оставить только один отзыв.
- Другие пользователи могут оставлять комметарии (Commentary) к отзыву.

____

## Как запустить проект

### Клонировать и развернуть репозиторий

```
git clone git@github.com:anywindblows/infra_actions.git
```

#### Выполните вход на свой удаленный сервер

#### Установите docker на сервер

```
sudo apt install docker.io 
```

#### Установите docker-compose на сервер(актуальная версия [тут](https://github.com/docker/compose/releases))

```
sudo curl -L "https://github.com/docker/compose/releases/download/v2.6.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```
```
sudo chmod +x /usr/local/bin/docker-compose
```
#### Скопируйте файлы docker-compose.yaml и nginx/default.conf из проекта на сервер

#### Добавьте в Secrets GitHub переменные окружения для работы

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

#### Запушить на Github. После успешного деплоя зайдите на боевой сервер и выполните команды

#### Собрать статические файлы в STATIC_ROOT

```
docker-compose exec web python3 manage.py collectstatic --noinput
```

#### Создать и применить миграции

```
docker-compose exec web python3 manage.py makemigrations
docker-compose exec web python3 manage.py migrate --noinput
```
### Документация проекта
```
https://github.com/anywindblows/api_yamdb/blob/master/README.md
```
