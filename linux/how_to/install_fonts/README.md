# Як встановити шрифти

Завантажте шрифт(и). (Наприклад [JetBrains Mono](https://www.jetbrains.com/lp/mono/))

Розпакуйте або скопіюйте файли **.ttf** у 

- `~/.local/share/fonts` (для поточного користувача), або у
- `/usr/share/fonts` (для всієї системи)

і запустіть:

{% include cl.htm cmd="fc-cache -f -v" %}
