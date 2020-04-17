# Перенести на сервер локальный репозиторий

Есть [такая инструкция](https://webhamster.ru/mytetrashare/index/mtb0/1339098198thylclyapv) ![ext][ext], но мне кажется, что мой метод проще.

## Как делаю я

Допустим, есть созревший проект: `/home/user/dev/project`, который мы хотим опубликовать.

На GitHub создаем репозиторий, например, такой `https://github.com/user/project.git`

На локальной машине временно "освободим" директорию проекта:

```
mv /home/user/dev/project /home/user/temp/project
```

Клонируем пустой репозиторий с сервера в директорию разработки:

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

[ext]: /i/link_ext.webp "External Link"
