# Jinja2

## Install

{% include cl.htm cmd="pip3 install Jinja2"
out="...
Successfully installed Jinja2-2.11.2 MarkupSafe-1.1.1" %}

На сервере, где установлено окружение (напр. python3.7), необходимо добавить опцию `--user`:

{% include cl.htm cmd="which pip3.7"
out="/usr/local/bin/pip3.7" %}

{% include cl.htm cmd="pip3.7 install Jinja2"
out="...
Could not install packages due to an EnvironmentError: [Errno 13] Permission denied...
Consider using the `--user` option or check the permissions." %}

{% include cl.htm cmd="pip3.7 install --user Jinja2"
out="...
Installing collected packages: MarkupSafe, Jinja2
Successfully installed Jinja2-2.11.2 MarkupSafe-1.1.1" %}

## Links

- https://pypi.org/project/Jinja2/
- <https://lectureswww.readthedocs.io/6.www.sync/2.codding/3.templates/jinja2.html>
