# Git

- [GitHub](github)
  - [Jekyll конструктор](github/pages/jekyll)
- [Книга Pro Git](#progit)

### Сокращенный вывод статуса

`-s` или `--short`

{% include cl.htm cmd="git status -s"
out=" M README
MM Rakefile
A  lib/git.rb
M  lib/simplegit.rb
?? LICENSE.txt
" %}

В выводе два столбца: в левом - статус, в правом - (не)модифицирован

- `??` - новые неотслеживаемые файлы
- <code>A&middot;</code> - файлы добавленные в отслеживаемые
- <code>&middot;M</code> - модифицирован и НЕ проиндексирован
- <code>M&middot;</code> - модифицирован и проиндексирован
- `MM` - модифицирован, проиндексирован и ещё раз модифицирован, т.е. на данный момент у него есть изменения которые попадут в коммит и те которые не попадут


{% include cl.htm cmd="git add file1.ext file2.ext ..." %}

{% include cl.htm cmd="git add --all" %}


#### TODO!


`git commit -m "description" filename.ext` | коммит только одного файла


#### Просмотр индексированных и неиндексированных изменений

{% include cl.htm cmd="git diff
git diff --staged
git diff --cached
" %}

#### Выбор программы для сравнения

Посмотреть, что уже установлено, и что можно можно установить:

{% include cl.htm cmd="git difftool --tool-help" %}

Установить для git программу сравнения, например, _meld_

{% include cl.htm cmd="git difftool --tool=meld" %}

#### Принудительно обновить отдаленный репозиторий:

{% include cl.htm cmd="git push -f origin master" %}

![!](/i/w.png) Но, следует понимать, что на сервере затрутся все изменения в файлах, которые были сделаны после последнего `git push`, даже если ты отправляешь всего один файл.

## <a href="progit"></a> Книга Pro Git

![Book](/i/b.png) [Pro Git](https://git-scm.com/book/ru/v2)

- [Запись изменений в репозиторий](https://git-scm.com/book/ru/v2/%D0%9E%D1%81%D0%BD%D0%BE%D0%B2%D1%8B-Git-%D0%97%D0%B0%D0%BF%D0%B8%D1%81%D1%8C-%D0%B8%D0%B7%D0%BC%D0%B5%D0%BD%D0%B5%D0%BD%D0%B8%D0%B9-%D0%B2-%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D0%B9)
- [Игнорирование файлов](https://git-scm.com/book/ru/v2/%D0%9E%D1%81%D0%BD%D0%BE%D0%B2%D1%8B-Git-%D0%97%D0%B0%D0%BF%D0%B8%D1%81%D1%8C-%D0%B8%D0%B7%D0%BC%D0%B5%D0%BD%D0%B5%D0%BD%D0%B8%D0%B9-%D0%B2-%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D0%B9#r_ignoring) см. также [.gitignore templates](https://github.com/github/gitignore)
- [Удаление больших объектов из истории](https://git-scm.com/book/ru/v2/Git-%D0%B8%D0%B7%D0%BD%D1%83%D1%82%D1%80%D0%B8-%D0%A3%D1%85%D0%BE%D0%B4-%D0%B7%D0%B0-%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D0%B5%D0%BC-%D0%B8-%D0%B2%D0%BE%D1%81%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5-%D0%B4%D0%B0%D0%BD%D0%BD%D1%8B%D1%85#r_removing_objects)
- [Работа с отдаленными репозиториями](https://git-scm.com/book/ru/v2/%D0%9E%D1%81%D0%BD%D0%BE%D0%B2%D1%8B-Git-%D0%A0%D0%B0%D0%B1%D0%BE%D1%82%D0%B0-%D1%81-%D1%83%D0%B4%D0%B0%D0%BB%D1%91%D0%BD%D0%BD%D1%8B%D0%BC%D0%B8-%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D1%8F%D0%BC%D0%B8)


## Другие ссылки

- [Изучаем команды pull и push](https://monsterlessons.com/project/lessons/git-izuchaem-komandy-pull-i-push)
- [7 советов по повышению производительности](https://nuancesprog.ru/p/5142/)
- [Очистить историю коммитов](https://www.shellhacks.com/ru/git-remove-all-commits-clear-git-history-local-remote/)




