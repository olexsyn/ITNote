# Security

- [Настройка SSL-сертификата LetsEncrypt](letsencrypt)


```apache
RewriteEngine on

# для хакерских запросов ищущих php-скрипты
RewriteCond %{REQUEST_URI} \.php$ [OR]
RewriteCond %{REQUEST_URI} admin
RewriteRule (.*) /error/404/hackers.htm [F,L]

# запросы по не защищенному протоколу и/или запросы с www
RewriteCond %{HTTPS} !on [OR]
RewriteCond %{HTTP_HOST} ^www\.
RewriteRule (.*) https://YOURDOMAIN.com%{REQUEST_URI} [L,R=301]
```
