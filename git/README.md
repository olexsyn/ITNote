# Git / GitHub

* [Git](#git)
* [GitHub](#github)
* [Jekyll](#jekyll)


## Git

- ![Book](/i/b.png) [Pro Git](https://git-scm.com/book/ru/v2)


### Запись изменений в репозиторий

[подробно](https://git-scm.com/book/ru/v2/%D0%9E%D1%81%D0%BD%D0%BE%D0%B2%D1%8B-Git-%D0%97%D0%B0%D0%BF%D0%B8%D1%81%D1%8C-%D0%B8%D0%B7%D0%BC%D0%B5%D0%BD%D0%B5%D0%BD%D0%B8%D0%B9-%D0%B2-%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D0%B9)

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


- [Ветки](branches)
- [Работа с удалёнными репозиториями](remote)
- [Работа с удалёнными репозиториями](https://git-scm.com/book/ru/v2/%D0%9E%D1%81%D0%BD%D0%BE%D0%B2%D1%8B-Git-%D0%A0%D0%B0%D0%B1%D0%BE%D1%82%D0%B0-%D1%81-%D1%83%D0%B4%D0%B0%D0%BB%D1%91%D0%BD%D0%BD%D1%8B%D0%BC%D0%B8-%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D1%8F%D0%BC%D0%B8)
- [.gitignore templates](https://github.com/github/gitignore)
- [Изучаем команды pull и push](https://monsterlessons.com/project/lessons/git-izuchaem-komandy-pull-i-push)

<a href="github"></a>

## GitHub

- [Перенести на сервер локальный репозиторий](repo2server)
- [Цвет шрифта и фона на GitHub Pages](pages_css)
- [GitHub Pages](pages)
- [GitHub Flavored Markdown](gfm)
- [GitHub Icons](github_icons)
- [Что такое pull request](http://ivan.rolik.name/2013/01/29/pull-request-without-fork-github/)
- [Как сделать свой первый Pull Request](https://rustycrate.ru/%D1%80%D1%83%D0%BA%D0%BE%D0%B2%D0%BE%D0%B4%D1%81%D1%82%D0%B2%D0%B0/2016/03/07/contributing.html)

<a href="jekyll"></a>

## Jekyll

- <https://jekyllrb.com/docs/>
- <https://frontender.info/build-blog-jekyll-github-pages/>
- <https://github.com/barryclark/jekyll-now> - <https://www.barryclark.co/>
