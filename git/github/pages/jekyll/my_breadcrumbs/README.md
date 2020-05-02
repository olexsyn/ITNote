# Мой breadcrumbs в шаблоне по умолчанию

_\_layouts/default.html_

```
[ 1]  {\% if page.title != "TechNote" %\}
[ 2]    {\% assign arr_pages = page.url | split: "/" %\}
[ 3]    {\% assign full_url = "" %\}
[ 4]    <p>
[ 5]    {\% for item in arr_pages %\}
[ 6]      {\% if item == '' %\}
[ 7]        <a href="{{ site.baseurl }}">home</a>
[ 8]        {\% assign full_url = full_url | append: site.baseurl %\}
[ 9]      {\% else %}
[10]        {\% assign full_url = full_url | append: "/" %\}
[11]        {\% assign full_url = full_url | append: item %\}
[12]        {\% assign dir = item | remove: ".html" %\}
[13]        / <a href="{{ full_url }}">{{ dir }}</a>
[14]      {\% endif %\}
[15]    {\% endfor %\}
[16]    </p>
[17]  {\% endif %\}
```
1. проверяем, если это первая (главная) страница, то 
2. 
3. 
4. 
5. 
6. 
7. 
8. 
9. 
10. 
11. 
12. 
13. 
14. 
15. 
16. 
17. 
