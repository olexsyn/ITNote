# Git

* [GitHub](github)
  * [Jekyll](github/jekyll)

- ![Book](/i/b.png) [Pro Git](https://git-scm.com/book/ru/v2)
  - [Удаление больших объектов из истории](https://git-scm.com/book/ru/v2/Git-%D0%B8%D0%B7%D0%BD%D1%83%D1%82%D1%80%D0%B8-%D0%A3%D1%85%D0%BE%D0%B4-%D0%B7%D0%B0-%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D0%B5%D0%BC-%D0%B8-%D0%B2%D0%BE%D1%81%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5-%D0%B4%D0%B0%D0%BD%D0%BD%D1%8B%D1%85#r_removing_objects)


### Запись изменений в репозиторий

[подробно](https://git-scm.com/book/ru/v2/%D0%9E%D1%81%D0%BD%D0%BE%D0%B2%D1%8B-Git-%D0%97%D0%B0%D0%BF%D0%B8%D1%81%D1%8C-%D0%B8%D0%B7%D0%BC%D0%B5%D0%BD%D0%B5%D0%BD%D0%B8%D0%B9-%D0%B2-%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D0%B9)

{% include cmdout.htm cmd="git status -s" out=" M README
MM Rakefile
A  lib/git.rb
M  lib/simplegit.rb
?? LICENSE.txt" %}

В выводе два столбца: в левом - статус, в правом - (не)модифицирован

- `??` - новые неотслеживаемые файлы
- `A&middot;` - файлы добавленные в отслеживаемые
- `M&middot;` - модифицирован и проиндексирован

- <pre>M&middot;</pre>
- <code>M&middot;</code>
- <samp>M&middot;</samp>

- `{{ site.baseurl }}`
- ```{{ site.baseurl }}```
- <pre>{{ site.baseurl }}</pre>
- <code>{{ site.baseurl }}</code>
- <samp>{{ site.baseurl }}</samp>


```
git status
git status -s
git status --short
```

```
git add file1.ext ... fileN.ext
git add --all
```

#### Просмотр индексированных и неиндексированных изменений

```
git diff
git diff --staged
git diff --cached
```

#### Выбор программы для сравнения

Посмотреть, что уже установлено, и что можно можно установить:

```git difftool --tool-help```

Установить для git программу сравнения, например, _meld_

```git difftool --tool=meld```

#### Принудительно обновить отдаленный репозиторий:

{% include cmdln.html comm="git push -f origin master" %}

Но, следует понимать, что на сервере затрутся все изменения в файлах, которые были сделаны после последнего `git push`, даже если ты отправляешь всего один файл.

- [Ветки](branches)
- [Работа с удалёнными репозиториями](remote)
- [Работа с удалёнными репозиториями](https://git-scm.com/book/ru/v2/%D0%9E%D1%81%D0%BD%D0%BE%D0%B2%D1%8B-Git-%D0%A0%D0%B0%D0%B1%D0%BE%D1%82%D0%B0-%D1%81-%D1%83%D0%B4%D0%B0%D0%BB%D1%91%D0%BD%D0%BD%D1%8B%D0%BC%D0%B8-%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D1%8F%D0%BC%D0%B8)
- [.gitignore templates](https://github.com/github/gitignore)
- [Изучаем команды pull и push](https://monsterlessons.com/project/lessons/git-izuchaem-komandy-pull-i-push)
- [7 советов по повышению производительности](https://nuancesprog.ru/p/5142/)




