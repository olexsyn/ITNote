# Подключение к GitHub через SSH

[help.github ... connecting-to-github-with-ssh](https://help.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh)

Используя протокол SSH, вы можете подключаться и аутентифицироваться на удаленных серверах и сервисах. С помощью ключей SSH вы можете подключаться к GitHub без указания имени пользователя или пароля когда отправляете локальные правки в GitHub-репозиторий.

Перед созданием ключа SSH вы можете проверить директорию **~/.ssh**, есть ли у вас какие-либо существующие ключи. По умолчанию имена открытых ключей имеют одно из следующих значений:

- id_rsa.pub
- id_ecdsa.pub
- id_ed25519.pub

## Создание ключей SSH

[help.github ... working-with-ssh-key-passphrases](https://help.github.com/en/articles/working-with-ssh-key-passphrases).

Если у вас нет пары открытых и закрытых ключей или вы не хотите использовать какие-либо из доступных для подключения к GitHub, то сгенерируйте новый ключ SSH, , используя указанный e-mail в качестве метки:

{% include cl.htm cmd='ssh-keygen -t rsa -b 4096 -C "your_email@example.com"'
out="
> Generating public/private rsa key pair.
> Enter a file in which to save the key (/home/you/.ssh/id_rsa): [Press enter]
> Enter passphrase (empty for no passphrase): [Type a passphrase]
> Enter same passphrase again: [Type passphrase again]
" %}

Когда вам будет предложено «Введите файл, в котором вы хотите сохранить ключ», нажмите Enter. Это принимает местоположение файла по умолчанию.

![!](/i/w.png) Также вы можете ввести безопасную ключевую фразу <samp>passphrase</samp>, но при этом она будет запрашиваться при сетевых операция с Git , как `push`, `pull` и `fetch`. Если вы хотите избежать необходимости вводить вашу парольную фразу каждый раз, вы можете использовать [ssh-agent для хранения учетных данных](../ssh-agent) парольной фразы личного ключа один раз за сеанс терминала.

## Добавление нового ключа SSH в вашу учетную запись GitHub

[help.github ... adding-a-new-ssh-key-to-your-github-account](https://help.github.com/en/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account)

Скопируйте ключ SSH в буфер обмена. Для этого достаточно скоприровать содержимое файла **~/.ssh/id_rsa.pub** в буфер обмена.

В правом верхнем углу страницы вашего GitHub-аккаунта нажмите на фотографию своего профиля, затем нажмите «Settings».

На боковой панели настроек пользователя нажмите на «SSH и GPG keys».

В поле «Title» добавьте описательную метку для нового ключа.

Вставьте свой ключ в поле «Key».

Нажмите «Add SSH key».

Если будет предложено, подтвердите свой пароль GitHub.

## Изменение протокола передачи данных репозитория с HTTP на SSH

[help.github ... switching-remote-urls](https://help.github.com/en/github/using-git/changing-a-remotes-url#switching-remote-urls-from-https-to-ssh)

Переходим в директорию необходимого репозитория

{% include cl.htm cmd="cd path/to/REPOSITORY" %}

Проверяем, что текущий протокол HTTP: "... _origin  https://_ ..."

{% include cl.htm cmd="git remote -v"
out="
origin  https://github.com/USERNAME/REPOSITORY.git (fetch)
origin  https://github.com/USERNAME/REPOSITORY.git (push)
" %}

Изменяем протокол:

{% include cl.htm cmd="git remote set-url origin git@github.com:USERNAME/REPOSITORY.git" %}

Проверяем, что протокол изменился на GIT: "... _origin  git@github.com:_"

{% include cl.htm cmd="git remote -v"
out="
origin  https://github.com/USERNAME/REPOSITORY.git (fetch)
origin  https://github.com/USERNAME/REPOSITORY.git (push)
" %}

Если ранее вводилась безопасная фраза-пароль, она может быть запрошена при командах `git pull`, `git push` и `git merge`.
