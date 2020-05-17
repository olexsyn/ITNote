## Файлы конфигураций

{% assign my_variable = 'TEXT' %}

- [fstab](fstab) 
- [crontab](crontab) <span class="r">TODO!</span>

`page.url` | {{ page.url }}
`page.path` | {{ page.path }}
`page.id` | {{ page.id }}
`page.dir` | {{ page.dir }}
`page.name` | {{ page.name }}
`page.categories` | {{ page.categories }}
`site.url` | {{ site.url }}
`site.baseurl` | {{ site.baseurl }}
`my_variable` | {{ my_variable }}

{% include f.htm f="config/README.md" %}

