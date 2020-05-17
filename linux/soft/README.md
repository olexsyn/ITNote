## Программы

{% assign abs_path = '/e-note/linux/soft' -%}

- [tar]({{ abs_path }}/tar)
- [rsync]({{ abs_path }}/rsync)
- [Sublime Text]({{ abs_path }}/sublime-text)
- [apt]({{ abs_path }}/apt) <span class="r">DELETE!</span>

`page.url` | {{ page.url }}
`page.path` | {{ page.path }}
`page.id` | {{ page.id }}
`page.dir` | {{ page.dir }}
`page.name` | {{ page.name }}
`page.categories` | {{ page.categories }}
`site.url` | {{ site.url }}
`site.baseurl` | {{ site.baseurl }}
`abs_path` | {{ abs_path }}

{% include f.htm f="soft/README.md" %}
