# Команды Linux

## Команды

- [mkdir](mkdir) - создать директорию

Несколько способов создать текстовый файл (пустой, с пустой строкой, с текстом):

{% include cl.htm
cmd='touch filename.ext
echo > filename.ext
echo "Some text" > filename.ext' %}

Еще вариант создать текстовый файл с текстом:

{% include cl.htm
cmd="cat > filename.ext"
out="Some text" %}

<kbd>Ctrl</kbd> + <kbd>D</kbd> - для сохранения и завершения редактирования.

TODO! nano
