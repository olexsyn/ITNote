# Подключить сайт

Конфигурационные файлы для виртуальных хостов хранятся в **/etc/apache2/sites-available/**

Для Apache, начиная с версии 2.4 у файла должно быть расширение `.conf`

Пример файла конфигурации хоста "mysite.com" (файл `/etc/apache2/sites-available/mysite_com.conf`):

```
  <VirtualHost *:80>
    ServerName mysite.com
    ServerAlias www.mysite.com
    DocumentRoot /var/www/mysite.com/www
  </VirtualHost>
```

Для того, что бы конфигурация читалась Апачем, нужно добавить ссылку на файл конфигурации хоста в **/etc/apache2/sites-enabled/**.

Сделать это можно командой `a2ensite`:

    sudo a2ensite mysite_com

Которая, на самом деле просто создает символическую ссылку:

    ln -s /etc/apache2/sites-available/mysite_com.conf /etc/apache2/sites-enabled/mysite_com.conf

И перезапустить сервер одной из команд:

{% include cl.htm cmd="sudo service apache2 reload
sudo systemctl reload apache2
sudo /etc/init.d/apache2 restart" out="
[ok] Restarting apache2 (via systemctl): apache2.service." %}

Команда для отключения конфигурации виртуального хоста: `a2dissite <SITE>`

В процессе запуска сервера можем получить сообщение:

`Could not reliably determine the server's fully qualified domain name, ...`

Это можем [испроавить так]({{ site.baseurl }}/apache/err_not_reliably_determine).
