# Linux

## Команды

[сбросить и снова включить своп](swap): <span class="r">TODO!</span>

{% include cl.htm cmd="sudo swapoff -a" %}

{% include cl.htm cmd="sudo swapon -a" %}

[установить разрешения на все каталоги или файлы](command/chmod_chown_r): <span class="r">TODO!</span>

{% include cl.htm cmd="find ./catalog -type d -exec chmod 755 {} \;" %}

{% include cl.htm cmd="find ./catalog -type f -exec chmod 644 {} \;" %}

[Создать с содержимым каталога / разархивировать tgz-архив](command/tar): <span class="r">TODO!</span>

{% include cl.htm cmd="tar -czf pages.tgz ./pages" %}

{% include cl.htm cmd="tar -xzf pages.tgz" %}

- [mkdir](command/mkdir)
- [сбросить страничный кэш](https://losst.ru/kak-osvobodit-pamyat-linux):

{% include_relative config/contents.md %}

{% include_relative soft/contents.md %}

## Разное

- [Размонтирование «занятого» устройства](https://p0vidl0.info/razmontirovanie-zanyatogo-ustrojstva.html)
