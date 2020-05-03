# Apache

- [Apache SSI](ssi)

## Установка

{% include cmd.htm cmd="sudo apt install apache2" %}

* [Apache HTTP Server Version 2.4 Documentation](http://httpd.apache.org/docs/2.4/)
  * [Introduction to Server Side Includes](http://httpd.apache.org/docs/2.4/howto/ssi.html)
  * [nginx в связке с ssi](http://nginx.org/ru/docs/http/ngx_http_ssi_module.html) - [nginx](http://nginx.org/ru/)

## Подключить сайт

Конфигурационные файлы для виртуальных хостов хранятся в _/etc/apache2/sites-available/_

Для Apache, начиная с версии 2.4 у файла должно быть расширение .conf

Пример файла конфигурации хоста "mysite.com" (файл _/etc/apache2/sites-available/mysite_com.conf_):
