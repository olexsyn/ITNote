## Команды

- [mkdir](mkdir) - создать директорию

[сбросить и снова включить своп](swap): <span class="r">TODO!</span>

{% include cl.htm
cmd="sudo swapoff -a
sudo swapon -a" %}

[установить разрешения на каталоги и файлы](command/chmod_chown_r): <span class="r">TODO!</span>

{% include cl.htm
cmd="find ./catalog -type d -exec chmod 755 {} \;
find ./catalog -type f -exec chmod 644 {} \;" %}

[Создать и разархивировать tgz-архив](command/tar): <span class="r">TODO!</span>

{% include cl.htm
cmd="tar -czf pages.tgz ./pages
tar -xzf pages.tgz" %}

Несколько способов создать текстовый файл (пустой, с пустой строкой, с текстом):

{% include cl.htm
cmd='touch filename.ext
echo > filename.ext
echo "Some text" > filename.ext' %}

Варианты создать текстовый файл с определенным текстом:

{% include cl.htm
cmd="cat > filename.ext"
out="Some text" %}

<kbd>Ctrl</kbd> + <kbd>D</kbd> - для сохранения и завершения редактирования.

{% include cl.htm
cmd="nano filename.ext" %}

<kbd>Ctrl</kbd> + <kbd>O</kbd> - сохранить, <kbd>Ctrl</kbd> + <kbd>X</kbd> - выйти из редактора

{% include f.htm f="command/README.md" %}
