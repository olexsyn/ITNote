## Программы

{% assign pid = '/linux/soft' -%}

- [tar]({{ pid }}/tar)
- [rsync]({{ pid }}/rsync)
- [Sublime Text]({{ pid }}/sublime-text)
- [apt]({{ pid }}/apt) <span class="r">DELETE!</span>

`page.url` | {{ page.url }}
`page.path` | {{ page.path }}
`page.id` | {{ page.id }}
`page.dir` | {{ page.dir }}
`page.name` | {{ page.name }}
`page.categories` | {{ page.categories }}
`site.url` | {{ site.url }}
`site.baseurl` | {{ site.baseurl }}
`abs_path` | abs_path

{% include f.htm f="pid/README.md" %}

https://github.com/olexsyn{{ site.baseurl }}/edit/master{{ pid }}/README.md
