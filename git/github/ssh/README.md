# Подключение к GitHub через SSH

[инструкция на англ.](https://help.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh)

Используя протокол SSH, вы можете подключаться и аутентифицироваться на удаленных серверах и сервисах. С помощью ключей SSH вы можете подключаться к GitHub без указания имени пользователя или пароля когда отправляете локальные правки в GitHub-репозиторий.

Перед созданием ключа SSH вы можете проверить директорию **~/.ssh**, есть ли у вас какие-либо существующие ключи. По умолчанию имена открытых ключей имеют одно из следующих значений:

- id_rsa.pub
- id_ecdsa.pub
- id_ed25519.pub

Если у вас нет пары открытых и закрытых ключей или вы не хотите использовать какие-либо из доступных для подключения к GitHub, то сгенерируйте новый ключ SSH:

{% include cmdout.htm cmd='ssh-keygen -t rsa -b 4096 -C "your_email@example.com"' out="> Generating public/private rsa key pair.
> Enter a file in which to save the key (/home/you/.ssh/id_rsa): [Press enter]
> Enter passphrase (empty for no passphrase): [Type a passphrase]
> Enter same passphrase again: [Type passphrase again]" %} 

