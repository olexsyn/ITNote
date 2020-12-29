## Ссылки



### Одна строка с командой

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
