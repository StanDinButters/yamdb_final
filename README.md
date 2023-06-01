# проект Yamdb API ![CI/CD](https://github.com/standinbutters/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)

Проект YaMDb собирает отзывы пользователей на произведения. Сами произведения в YaMDb не хранятся, здесь нельзя посмотреть фильм или послушать музыку.
Произведения делятся на категории, такие как «Книги», «Фильмы», «Музыка». Например, в категории «Книги» могут быть произведения «Винни-Пух и все-все-все» и «Марсианские хроники», а в категории «Музыка» — песня «Давеча» группы «Жуки» и вторая сюита Баха. Список категорий может быть расширен (например, можно добавить категорию «Изобразительное искусство» или «Ювелирка»).

Произведению может быть присвоен жанр из списка предустановленных (например, «Сказка», «Рок» или «Артхаус»).
Добавлять произведения, категории и жанры может только администратор.

Благодарные или возмущённые пользователи оставляют к произведениям текстовые отзывы и ставят произведению оценку в диапазоне от одного до десяти (целое число); из пользовательских оценок формируется усреднённая оценка произведения — рейтинг (целое число). На одно произведение пользователь может оставить только один отзыв.
Пользователи могут оставлять комментарии к отзывам.
Добавлять отзывы, комментарии и ставить оценки могут только аутентифицированные пользователи.

### Стек технологий:

- Python 3.7
- Django 2.2
- Django REST framework
- Django rest_framework_simplejwt
- Gunicorn
- Nginx
- PostgreSQL
- Git
- Docker

## Ресурсы API YaMDb

Ресурс **users**: пользователи.

Ресурс **auth**: аутентификация.

Ресурс **titles**: произведения, к которым пишут отзывы.

Ресурс **categories**: категории (типы) произведений.

Ресурс **comments**: комментарии к отзывам.

Ресурс **genres**: жанры произведений..

Ресурс **reviews**: отзывы на произведения.

#### Подготовка сервера:

Войти на свой удаленный сервер.
Установить Docker и docker-compose.

```commandline
sudo apt install docker.io
```

```commandline
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

```commandline
sudo chmod +x /usr/local/bin/docker-compose
```

Из паки `infra` локального проекта cкопировать на сервер в домашнюю дирректорию файлы настроек nginx и docker-compose

```commandline
scp docker-compose.yaml <USER>@<HOST>:/home/<USER>
```

```commandline
scp ./nginx/default.conf <USER>@<HOST>:/home/<USER>/nginx/
```

1.Запустить сборку и запуск контейнеров:
```sh
sudo docker-compose up -d --build
```
2.Выполнить миграции:
```sh
sudo docker-compose exec web python manage.py migrate
```
3.Выполнить сбор статических файлов:
```sh
sudo docker-compose exec web python manage.py collectstatic --no-input
```
4.Создать суперпользователя:
```sh
sudo docker-compose exec web python manage.py createsuperuser
```
### Команды для заполнения базы данными

запускаем команду для загрузки баз
```
sudo docker-compose exec web python manage.py loaddata fixtures.json
```

Проверьте работу, перейдя по ссылке: [http://51.250.82.32/admin/](http://51.250.82.32/admin/)
</br></br>
Для остановки контейнера используется команда:
```
sudo docker-compose down -v
```
## Rest-API

Документацию по API доступна по ссылке [http://51.250.82.32/redoc/](http://51.250.82.32/redoc/)