## Ссылки

### Абсолютные и относительные

Можно указать абсолютную, "от корня", но при этом, нужно использовать переменную _site.baseurl_:

{% raw %}
```
[Apt]({{ site.baseurl }}/linux/soft/apt/)
```
{% endraw %}

или оносительную, от текущей директории:

{% raw %}
```
[Apt](../../soft/apt/)
```
{% endraw %}


### Мои ссылки

Для того, чтобы ссылки на другие сайты открывались в новом окне прописал в `e-note/_includes/a.htm` такой код

{% raw %}
```html
<a href="{{ include.url }}" target="_blank" rel="nofollow">
{%- if include.text -%}
  {{ include.text }}
{%- else -%}
  {{ include.url }}
{%- endif -%}
</a>
```
На страницах ссылка оформляется так:

```
{% include a.htm url="https://github.com" %}
```
{% endraw %}

Для отличия по цвету (зеленые - мои, синие - чужие) в css:

```css
a {
	color: green;
	text-decoration: none
}

a[href ^= "http"] {
  color: #0366d6;
}

a[href ^= "mailto"] {
  color: #0366d6;
}
```


{% include f.htm f="links.md" %}
