# Test

{% include constants.htm -%}

{% raw %}
```
{% include warn.htm text="INFO" color ="blue" %}
<span class="r">Only RED!</span>
```
{% endraw %}

{% include warn.htm text="INFO" color ="blue" %}

<span class="r">Only RED!</span>

<span class="warn">?</span> question

<span class="info">info</span> info

<span class="dang">!</span> danger

## Contents

- [code](#code)
- [images](#images)
- [test](#test2)
- [Разное](#разное)

---

<a name="code"></a>
{% include_relative code.md %}

<a name="images"></a>
{% include_relative images_example.md %}

<a name="test2"></a>
{% include_relative test2.md %}


{% include_relative different.md %}


