## Файлы конфигураций

{% assign abs_path = '/e-note/linux/config' -%}

- [fstab]({{abs_path}}/fstab) 
- [crontab]({{abs_path}}/crontab) <span class="r">TODO!</span>

`page.url` | {{ page.url }}
`page.path` | {{ page.path }}
`page.id` | {{ page.id }}
`page.dir` | {{ page.dir }}
`page.name` | {{ page.name }}
`page.categories` | {{ page.categories }}
`site.url` | {{ site.url }}
`site.baseurl` | {{ site.baseurl }}
`abs_path` | {{ abs_path }}

{% include f.htm f="config/README.md" %}

