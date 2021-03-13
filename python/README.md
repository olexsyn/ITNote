# Python

- [Синтаксис](syntax)
- [Модули](modules)
- [Библиотеки](library)
- [Работа с файлами](files)

## Строки
- {% include a.htm url="https://pythonru.com/osnovy/stroki-python" text="Строки в python 3: методы, функции, форматирование" %}
- {% include a.htm url="https://pythonru.com/osnovy/formatirovanie-v-python-s-pomoshhju-format" text="Форматирование строк с помощью format()" %}
- {% include a.htm url="https://pythonru.com/primery/10-primerov-ispolzovanija-metodov-stok-v-python" text="10 примеров использования методов строк в python" %}

---

- {% include a.htm url="https://pythonru.com/primery/kak-ispolzovat-modul-datetime-v-python" text="Как использовать модуль datetime" %}
- {% include a.htm url="https://pythonru.com/primery/asinhronnost-python-na-primere" text="Асинхронность python на примере asyncio" %}
- {% include a.htm url="https://proglib.io/p/python-docs/" text="Работа с документацией в Python: поиск информации и соглашения" %}
- {% include a.htm url="https://habr.com/ru/post/417783/" text="Списки VS кортежи. Оптимизации" %}
- {% include a.htm url="https://pythonworld.ru/tipy-dannyx-v-python/isklyucheniya-v-python-konstrukciya-try-except-dlya-obrabotki-isklyuchenij.html" text="Конструкция try - except для обработки исключений" %}
- {% include a.htm url="https://ru.stackoverflow.com/questions/460207/%D0%95%D1%81%D1%82%D1%8C-%D0%BB%D0%B8-%D0%B2-python-%D0%BE%D0%BF%D0%B5%D1%80%D0%B0%D1%82%D0%BE%D1%80-switch-case" text="Есть ли в Python оператор switch case?" %}
- {%  include a.htm url="https://pbpython.com/pdf-reports.html" text="Creating PDF Reports with Pandas, Jinja and WeasyPrint" %}

- [Форма + AJAX](form_ajax)

- [Отправка e-mail](email)
- [Примеры CGI](cgi-examples)
- [Удаление дубликатов из списка. Сохранить порядок элементов](remove_dubl)

## Завершение программ

```python
sys.exit(code)  # code - не обязателен
```

```python
os._exit(code)  # code - необходим!
```
''code'' = **0** - нормальное завершение; другие значения, если возникли проблемы

[подробнее](exit)


## Ошибки

* `malformed header from script 'script.py': Bad header: NameError, referer: http://...`

Скрипт в терминале отрабатывает без ошибок, а в браузере получаем Error 500.

Одна из причин: вероятно, что скрипт пишет в лог. И когда запуск производился через терминал, то файл лога создался владельцем текущей учетной записи. При запуске через http, владелец уже `www-data` который не имеет прав записи в этот файл. Нужно просто удалить файл лога и запустить скрипт через http еще раз.

* `python3: Relink '/lib/x86_64-linux-gnu/libsystemd.so.0' with '/lib/x86_64-linux-gnu/librt.so.1' for IFUNC symbol 'clock_gettime'`

Скрипт в терминале показывает это сообщение, а в браузере получаем Error 500.

Аналогичная предыдущей проблема, возникающая при подключении модуля логирования logging, при настройке записи в файл, который уже создан от другого пользователя. Удалить файл лога или назначить ему разрешение 777.
