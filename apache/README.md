# Apache

- Установка
- [SSI](ssi)
- [ModRewrite](mod_rewrite)
- [SSL](ssl)
- [Коды ошибок](error_code)
- [Проблема корректного отображения UTF8 в CGI-скриптах](cgi-utf-fix)
- [Apache і Мирохост](mirohost)
- [Проблема с SSI в связке Apache и Nginx на Mirohost](mirohost_ssi_nginx)

## Версия, стоп, старт, рестарт

{% include cl.htm cmd="/usr/sbin/apache2 -v"
out="Server version: Apache/2.4.29 (Ubuntu)
Server built:   2020-03-13T12:26:16"
%}

{% include cl.htm cmd="service apache2 stаtus" %}

{% include cl.htm cmd="sudo service apache2 stop|start|restart" %}

а также, в некоторых дистрибутивах Linux:

{% include cl.htm cmd="sudo systemctl stop|start|restart httpd.service
systemctl status httpd" %}

{% include cl.htm cmd="/etc/init.d/apache2 status
/etc/init.d/apache2 stop|start|restart|reload|force-reload" %}

{% include cl.htm cmd="apache2ctl configtest" %}  

выводит ошибку в конфиге Apache. Помогает
понять, где напортачено в файлах конфигурации

<span class="warn">!</span> В случае появления сообщения `AH00558: httpd: Could not reliably determine the server's fully qualified` необходимо прописать `ServerName localhost` в файле **/etc/apache2/apache2.conf** (или **/etc/httpd/conf/httpd.conf**)

## restart и reload - разница?

- **restart**: останавливает (**stop**), а затем запускает (**start**) службу Apache.
- **reload:** изящно перезапускает службу Apache. При reload основной процесс Apache завершает работу дочерних процессов, загружает новую конфигурацию и запускает новые дочерние процессы.

## Установка

{% include cl.htm cmd="sudo apt install apache2" %}

- [Apache HTTP Server Version 2.4 Documentation](http://httpd.apache.org/docs/2.4/)
  - [Introduction to Server Side Includes](http://httpd.apache.org/docs/2.4/howto/ssi.html)
  - [nginx в связке с ssi](http://nginx.org/ru/docs/http/ngx_http_ssi_module.html) - [nginx](http://nginx.org/ru/)

- [Apache SSI](ssi)
- [Подключить SSI - a2enmod](a2enmod)
- [Как подключить mod_rewrite](mod_rewrite)

## Подключить виртуальный хост

Начиная с версии 2.4 у конфигурационного файла виртуального хоста должно быть расширение `.conf`.
Пример файла конфигурации хоста test.net (файл **/etc/apache2/sites-available/test.net.conf**):

```apache
<VirtualHost 127.0.1.2:80>
	ServerName test.net.loc
	DocumentRoot /home/olex/www/test.net/test.net
	<Directory /home/olex/www/test.net/test.net/>
		Options +Includes
		AddType text/html .htm
		AddOutputFilter INCLUDES .htm
		AllowOverride All
		Require all granted
	</Directory>

	ScriptAlias /cgi-bin/ /home/olex/www/test.net/cgi-bin/
	<Directory "/home/olex/www/test.net/cgi-bin">
		AllowOverride None
		Options +ExecCGI -MultiViews
		Require all granted
	</Directory>

	ErrorLog /home/olex/www/__logs/test.net/error.log
	CustomLog /home/olex/www/__logs/test.net/access.log combined
</VirtualHost>
```

{% include cl.htm cmd="sudo a2ensite test.net
service apache2 reload" %}


---


<span class="warn">TODO!</span>

- [Подключить виртуальный хост - a2ensite](a2ensite)
- [Configuring Apache2 to run Python Scripts](https://www.linux.com/training-tutorials/configuring-apache2-run-python-scripts/)
