# Linux


- [Проблемы](#trouble)



## Команды

[сбросить и снова включить своп](swap): <span class="r">TODO!</span>

{% include cl.htm cmd="sudo swapoff -a
sudo swapon -a" %}

[установить разрешения на каталоги и файлы](command/chmod_chown_r): <span class="r">TODO!</span>

{% include cl.htm cmd="find ./catalog -type d -exec chmod 755 {} \;
find ./catalog -type f -exec chmod 644 {} \;" %}

[Создать и разархивировать tgz-архив](command/tar): <span class="r">TODO!</span>

{% include cl.htm cmd="tar -czf pages.tgz ./pages
tar -xzf pages.tgz" %}

- [mkdir](command/mkdir)
- [сбросить страничный кэш](https://losst.ru/kak-osvobodit-pamyat-linux):

{% include_relative config/contents.md %}

{% include_relative soft/contents.md %}


<a name="trouble"></a>
{% include_relative trouble/README.md %}


## Разное

- [Размонтирование «занятого» устройства](https://p0vidl0.info/razmontirovanie-zanyatogo-ustrojstva.html)
