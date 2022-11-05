![example workflow](https://github.com/github/docs/actions/workflows/yamdb_workflow.yml/badge.svg)


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

### Клонировать репозиторий и перейти в него в командной строке

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

#### Затем необходимо задать правильные разрешения, чтобы сделать команду docker-compose исполняемой

```
sudo chmod +x /usr/local/bin/docker-compose
```

#### Скопируйте файлы docker-compose.yaml и nginx/default.conf из проекта на сервер

```
scp docker-compose.yaml <username>@<host>:/home/<username>/docker-compose.yaml
```

```
scp -r nginx <username>@<host>:/home/<username>/
```

#### Добавьте в Secrets GitHub переменные окружения для работы

```
DB_ENGINE=django.db.backends.postgresql
DB_HOST=db
DB_NAME=postgres
DB_PASSWORD=postgres
DB_PORT=5432
DB_USER=postgres

DOCKER_PASSWORD=<Docker password>
DOCKER_USERNAME=<Docker username>

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

#### Применить миграции

```
docker-compose exec web python3 manage.py migrate --noinput
```

#### Заполнить базу данных

```
docker-compose exec web python3 manage.py loaddata fixtures.json
```

#### Создать суперпользователя Django

```
docker-compose exec web python manage.py createsuperuser
```