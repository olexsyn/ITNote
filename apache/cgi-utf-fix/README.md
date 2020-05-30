Решение проблемы корректного отображения символов UTF8 при выполнении CGI-скриптов

Проблема:

**TODO!** 

Простой скрипт на perl или python, запускаемый, как cgi, некорректно выводят кириллицу (и другие utf символы тоже).

```perl
#!/usr/bin/perl

print("Content-Type: text/html\n\n");
print("Привет, МИР!");
```

```python
#!/usr/bin/python3

print("Content-Type: text/html\n")
print("Привет, МИР!")
```

Всякие decode/encode не помогают. Прописывание кодировок по умолчанию в **.htaccess** - тоже

HTML-страница выводится в кодировке `ANSI_X3.4-1968`

Решение:

<small><a href=https://stackoverflow.com/questions/9322410/set-encoding-in-python-3-cgi-scripts" target="_blank"></small>

1\. В файле **/etc/apache2/envvars** раскоментировать (если закоментирована) строку
```
#. /etc/default/locale
```

2\. В конфирурационном файле виртуального хоста в разделе _ScriptAlias/Directory_ прописать строку `PassEnv LANG en_US.UTF-8`:

```apache
	ScriptAlias /cgi-bin/ /www/example.com/cgi-bin/
	<Directory "/www/example.com/cgi-bin">
		...
		Options +ExecCGI -MultiViews
		PassEnv LANG en_US.UTF-8
		...
	</Directory>
```

3\. В выводимый заголовок `Content-Type` CGI-скрипта добавлять кодировку `utf-8`

```python
print("Content-Type: text/html; charset=utf-8\n\n");  # Perl

print('Content-Type: text/html; charset=utf-8\n')  # Python
```
