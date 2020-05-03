# Мой breadcrumbs в шаблоне по умолчанию

Код, который построит breadcrumb, расположим в _\_includes\breadcrumb.htm_, и подключим его к шаблону _\_layouts/default.html_:
{% comment %}
```
{% include breadcrumb.htm %}
```

Вот содержимое файла _breadcrumb.htm_
```
[ 1]{% if page.url != "/" %}
[ 2]	{% assign arr_pages = page.url | split: "/" %}
[ 3]	{% assign last_page = page.url | split: "/" | last %}
[ 4]	{% assign full_url = "" %}
[ 5]	<p>
[ 6]	{% for item in arr_pages %}
[ 7]		{% if item == '' %}
[ 8]			<a href="{{ site.baseurl }}">home</a>
[ 9]			{% assign full_url = full_url | append: site.baseurl %}
[10]		{% else %}
[11]			{% assign full_url = full_url | append: "/" %}
[12]			{% assign full_url = full_url | append: item %}
[13]			{% assign dir = item | remove: ".html" %}
[14]			{% if dir == last_page %}
[15]				/ <b>{{ dir }}</b>
[16]			{% else %}
[17]				/ <a href="{{ full_url }}">{{ dir }}</a>
[19]			{% endif %}
[20]		{% endif %}
[21]	{% endfor %}
[22]	</p>
[23]{% endif %}
```
{% endcomment %}

## Вступительное пояснение

Итак, пусть, например, наш путь к текущей странице выглядит так: _/repname/first/second/third_

Наш breadcrumb (цепочка страниц) будет выглядеть так:

<samp>home / first / second / third</samp>

, где каждая страничка будет в виде ссылки на саму себя.

При этом, в служебной переменной `site.baseurl` будет находиться _/repname_ (т.е. home),

а в служебной переменной `page.url` - цепочка пути _/first/second/third_.

Конечно же, вместо <samp>home</samp>, можно указывать, что угодно: <samp>index</samp>, <samp>root</samp>, изобразить в виде домика, или присвоить имя репозитория. Но в этом примере - это <samp>home</samp>.


## Как работает код

1. проверяем, если это не первая (главная) страница, то выполняем код
2. разделяем текущий URL страницы по символу "/" и создаем массив `arr_pages=['','first','second','third']`. Обрати внимание, что первый элемент будет всегда пустой, т.к. мы разбиваем URL по "слешам", а URL начинается со "слеша"!
3. в переменную `last_page` мы заносим имя последней страницы в цепочке, т.е. _third_
4. подготавливаем переменную `full_url`, которая поочередно будет принимать значение пути к каждой странице в цепочке
5. начинаем формировать и выводить код breadcrumb'а
6. для каждого элемента массива `arr_pages` проверяем...
7. ... не пустой ли он? А первый элемент всегда пустой, в т.ч. даже если он и одновременно и последний - в случае когда мы находимся в корне сайта.
8. поэтому, формируем первую ссылку - <samp>home</samp>
9. присваиваем переменной `full_url` значение корня - `site.baseurl`. Если мы укажем `/`, то попадем в корень _username.github.io_, а надо на _username.github.io/repname_, поэтому и корень для нас - `site.baseurl`
10.
11.
12.
13.
14.
15.
16.
17.
