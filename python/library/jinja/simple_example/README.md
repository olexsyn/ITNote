# Простой пример cgi-скрипта подключающего шаблон Jinja

**Главный шаблон** /home/user/local/test.net/_tpl/**test.htm**

{% raw -%}
```html
<!DOCTYPE html>
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <title>Test Jinja</title>
  </head>
  <body>
  	{% include '_nav.htm' %}
    <h3>Test 2 Jinja</h3>
    {%- for item in range(5) %}
      <p>Hello {{ user }}!</p>
    {%- endfor %}
    {% include '_footer.htm' %}
  </body>
</html>
```

**Шаблон** /home/user/local/test.net/_tpl/**_nav.htm**

```html
<nav>
    <a href="/home">{{ home }}</a>
    <a href="/blog">Blog</a>
    <a href="/contact">Contact</a>
</nav>
```

**Шаблон** /home/user/local/test.net/_tpl/**_footer.htm**

```html
<hr>
<p>Copyright {{ corp }}</p>
```
{%- endraw %}

**CGI-скрипт**



**Вывод в браузер:**

```html
<!DOCTYPE html>
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <title>Test Jinja</title>
  </head>
  <body>
  	<nav>
    <a href="/home">Home Page</a>
    <a href="/blog">Blog</a>
    <a href="/contact">Contact</a>
</nav>
    <h3>Test 2 Jinja</h3>
      <p>Hello Вася!</p>
      <p>Hello Вася!</p>
      <p>Hello Вася!</p>
      <p>Hello Вася!</p>
      <p>Hello Вася!</p>
    <hr>
<p>Copyright Копирайт</p>
  </body>
</html>
```
