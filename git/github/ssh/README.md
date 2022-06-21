# Подключение к GitHub через SSH

[help.github ... connecting-to-github-with-ssh](https://help.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh)

Используя протокол SSH, вы можете подключаться и аутентифицироваться на удаленных серверах и сервисах. С помощью ключей SSH вы можете подключаться к GitHub без указания имени пользователя или пароля когда отправляете локальные правки в GitHub-репозиторий.

Перед созданием ключа SSH вы можете проверить директорию **~/.ssh**, есть ли у вас какие-либо существующие ключи. По умолчанию имена открытых ключей имеют одно из следующих значений:

- id_rsa.pub
- id_ecdsa.pub
- id_ed25519.pub

## Создание ключей SSH

[help.github ... working-with-ssh-key-passphrases](https://help.github.com/en/articles/working-with-ssh-key-passphrases).

Якщо у вас немає пари відкритих і закритих ключів або ви не хочете використовувати будь-які доступні для підключення до GitHub, то згенеруйте новий ключ SSH, використовуючи свій e-mail як ідентифікатор:

{% include cl.htm cmd='ssh-keygen -t ed25519 -C "mylogin@example.com"' %}

> Примітка. Якщо ви використовуєте застарілу систему, яка не підтримує алгоритм Ed25519, використовуйте:
> `$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`

У вас буде запитано ім'я файлу (треба вводити повний шлях, бажано у `/home/user/.ssh/`), та пароль

{% include cl.htm cmd='ssh-keygen -t ed25519 -C "mylogin@example.com"'
out="Generating public/private ed25519 key pair.
Enter file in which to save the key (/home/olex/.ssh/id_ed25519): /home/olex/.ssh/mylogin
Created directory '/home/olex/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/olex/.ssh/mylogin
Your public key has been saved in /home/olex/.ssh/mylogin.pub
The key fingerprint is:
SHA256:DALKyEu8zwu08jo3gPcUVjmrjOXpP4wSUy27jQHNKf5 mylogin@example.com
The key's randomart image is:
+--[ED25519 256]--+
|. .o=..          |
|*o o.=.          |
|++o +.o          |
|. .. = o .       |
| .  . + S        |
|   . + =         |
|    o.E..        |
|    +@oO+        |
|   o++X=*o       |
+----[SHA256]-----+
" %}

Коли вам буде запропоновано «Введіть файл, у якому потрібно зберегти ключ», натисніть Enter. Це приймає розташування файлу за замовчуванням.

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
