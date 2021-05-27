## Ссылки

### Абсолютные и относительные

Можно указать абсолютную, "от корня", но при этом, нужно использовать переменную _site.baseurl_:

{% raw %}
[Apt]({{ site.baseurl }}/linux/soft/apt/)
{% endraw %}

или оносительную от текущей директории:

{% raw %}
[Apt](../../soft/apt/)
{% endraw %}


### Мои ссылки

{% raw %}
```
<a href="{{ include.url }}" target="_blank" rel="nofollow">
{%- if include.text -%}
  {{ include.text }}
{%- else -%}
  {{ include.url }}
{%- endif -%}
</a>
```

```
{% include a.htm url="https://github.com" %}
```
{% endraw %}



{% include f.htm f="links.md" %}
