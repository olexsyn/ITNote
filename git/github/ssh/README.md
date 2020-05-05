# Подключение к GitHub через SSH

[инструкция на англ.](https://help.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh)

Используя протокол SSH, вы можете подключаться и аутентифицироваться на удаленных серверах и сервисах. С помощью ключей SSH вы можете подключаться к GitHub без указания имени пользователя или пароля когда отправляете локальные правки в GitHub-репозиторий.

Перед созданием ключа SSH вы можете проверить директорию **~/.ssh**, есть ли у вас какие-либо существующие ключи. По умолчанию имена открытых ключей имеют одно из следующих значений:

- id_rsa.pub
- id_ecdsa.pub
- id_ed25519.pub

## Создание ключей SSH

Если у вас нет пары открытых и закрытых ключей или вы не хотите использовать какие-либо из доступных для подключения к GitHub, то сгенерируйте новый ключ SSH:

{% include cmdout.htm cmd='ssh-keygen -t rsa -b 4096 -C "your_email@example.com"' out="> Generating public/private rsa key pair.
> Enter a file in which to save the key (/home/you/.ssh/id_rsa): [Press enter]
> Enter passphrase (empty for no passphrase): [Type a passphrase]
> Enter same passphrase again: [Type passphrase again]" %} 

Это создаст новый ключ ssh, используя предоставленный e-mail в качестве метки.

Когда вам будет предложено «Введите файл, в котором вы хотите сохранить ключ», нажмите Enter. Это принимает местоположение файла по умолчанию.

Вы можете ввести безопасную фразу-пароль <samp>passphrase</samp>. Для получения дополнительной информации см. «[Работа с паролями в SSH](https://help.github.com/en/articles/working-with-ssh-key-passphrases)».

## Добавление вашего SSH-ключа в ssh-agent

Запустите ssh-agent в фоновом режиме.

{% include cmdout.htm cmd='$ eval "$(ssh-agent -s)"' out="> Agent pid 59566" %} 

Добавьте свой закрытый ключ SSH в ssh-agent. Если вы создали свой ключ с другим именем, или если вы добавляете существующий ключ с другим именем, замените в команде id_rsa именем вашего файла закрытого ключа.

{% include cmd.htm cmd="$ ssh-add ~/.ssh/id_rsa" %} 

## Добавление нового ключа SSH в вашу учетную запись GitHub

Скопируйте ключ SSH в буфер обмена. Для этого достаточно скоприровать содержимое файла **~/.ssh/id_rsa.pub** в буфер обмена.

В правом верхнем углу страницы вашего GitHub-аккаунта нажмите на фотографию своего профиля, затем нажмите «Settings».

На боковой панели настроек пользователя нажмите на «SSH и GPG keys». 

В поле «Title» добавьте описательную метку для нового ключа.

Вставьте свой ключ в поле «Key».

Нажмите «Add SSH key». 

Если будет предложено, подтвердите свой пароль GitHub. 

## Изменение протокола передачи данных репозитория с HTTP на SSH

[help.github.com](https://help.github.com/en/github/using-git/changing-a-remotes-url#switching-remote-urls-from-https-to-ssh)

Переходим в директорию необходимого репозитория

{% include cmd.htm cmd="cd path/to/REPOSITORY" %}

Проверяем, что текущий протокол HTTP: "... _origin  https://_ ..."

{% include cmdout.htm cmd="git remote -v"
out="origin  https://github.com/USERNAME/REPOSITORY.git (fetch)
origin  https://github.com/USERNAME/REPOSITORY.git (push)" %}

Изменяем протокол:

{% include cmd.htm cmd="git remote set-url origin git@github.com:USERNAME/REPOSITORY.git" %}

Проверяем, что протокол изменился на GIT: "... _origin  git@github.com:_"

{% include cmdout.htm cmd="git remote -v"
out="origin  https://github.com/USERNAME/REPOSITORY.git (fetch)
origin  https://github.com/USERNAME/REPOSITORY.git (push)" %}

Если ранее вводилась безопасная фраза-пароль, она может быть запрошена при командах `git pull` и `git push`.
