# call

Вы можете легко отображать сообщения системные всплывающие уведомления из программ на Python или любом другом языке.

Вам понадобится обвязка **libnotify** для Python:

    pacman -S python-notify

<small>(pacman - установщик для Archlinux, Manjaro)</small>

Вот простой "hello world" пример:

```python
import subprocess

info = "Hello world!"
subprocess.call(['notify-send', info])
```
