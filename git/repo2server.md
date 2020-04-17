# Перенести на сервер локальный репозиторий

Есть [такая инструкция](https://webhamster.ru/mytetrashare/index/mtb0/1339098198thylclyapv), но мне кажется, что мой метод проще.

## Как делаю я

Допустим, есть созревший для публикации проект: `/home/user/dev/project`, который мы хотим положить на GitHub.

На GitHub создаем репозиторий с файлом `README.md`, например, такой `https://github.com/user/project.git`

На локальной машине временно "очистим"" директорию проекта:

```
mv /home/user/dev/project /home/user/temp/project
```

Клонируем репозиторий с сервера (там только файл README.md) в директорию разработки:

```
cd /home/user/dev
git clone https://github.com/user/project.git
```

И перемещаем наш проект на место:

```
mv /home/user/temp/project /home/user/dev/project
```

Далее, индексируем, коммитим, забрасываем на сервер:

```
git add --all
git commit -m "Welcome GitHub!"
git push origin master
```

Все!