Текущая директория и директория скрипта
=======================================

Если вы запускаете скрипт `C:\Scripts\script.py` из `D:\work` папки:

    D:\work> py C:\Scripts\script.py

то:

- `D:\work` — это текущая рабочая директория на момент старта скрипта. (Напр.: `open('file.txt')` будет пытаться открыть `D:\work\file.txt` файл)
- `C:\Scripts` — это директория со скриптом.

Текущая рабочая директория
--------------------------

Текущая рабочая директория возвращается функцией [os.getcwd()](https://docs.python.org/3/library/os.html#os.getcwd), где `CWD` это Current Working Directory ("текущая рабочая директория"). `os.getcwdb()` возвращает путь в виде байт. Происхождение функции от [POSIX getcwd(3)](https://pubs.opengroup.org/onlinepubs/9699919799/functions/getcwd.html). Другие способы могут вернуть разные результаты в зависимости от настроек доступа промежуточных директорий, общей длины (зависит от платформы) и т.д. — не изобретайте своих способов, если не осознаете всех последствий возможного изменения в поведении функции. Также нетрадиционные способы получения рабочей директории могут ухудшить читаемость другими Питон-программистами.

По умолчанию относительные пути используют именно эту директорию, поэтому вызывать 'os.getcwd()' обычно не приходится. Например, `open('file.txt')` вызов открывает файл 'file.txt' в текущей директории. Если необходимо передать полный путь в виде строки, то можно использовать `os.path.abspath('file.txt')` — `getcwd()` снова явно не используется.

[Path.cwd() из модуля pathlib](https://docs.python.org/3/library/pathlib.html#pathlib.Path.cwd) возвращает путь к текущей директории как объект c разными полезными и удобными методами такими как `.glob('**/*.py')`.

Директория со скриптом
----------------------

Текущая рабочая директория может отличаться от директории с текущим python-скриптом. Можно использовать `os.path.dirname(os.path.abspath(__file__))`, чтобы получить директорию со скриптом, но это работает не всегда. Посмотрите на `get_script_dir()` функцию, которая поддерживает более общий случай:

```python
import inspect
import os
import sys

def get_script_dir(follow_symlinks=True):

	if (sys, 'frozen', False):  # py2exe, PyInstaller, cx_Freeze
		path = os.path.abspath(sys.executable)
		print('1',path)
	else:
		path = inspect.getabsfile(get_script_dir)
		print('2',path)

	if follow_symlinks:
		path = os.path.realpath(path)
		print('3',path)

	return os.path.dirname(path)


print(get_script_dir())
```

Если хочется получить данные из файла, расположенного относительно установленного Питон-модуля, то используйте [pkgutil.get_data()](https://docs.python.org/3/library/pkgutil.html#pkgutil.get_data) или [setuptools pkg_resources.resource_string()](https://setuptools.readthedocs.io/en/latest/pkg_resources.html#resourcemanager-api) вместо построения путей c помощью `__file__`. Это работает даже, если ваш пакет упакован в архив. В Python 3.7 появился модуль `importlib.resources`. К примеру, если у вас есть Питон-пакет `data` внутри которого лежит `файл.txt`, то чтобы достать текст:

```python
import importlib.resources
text = importlib.resources.read_text('data', 'файл.txt') 
```

Если вы хотите найти место куда пользовательские данные можно положить, то модуль [appdirs](https://pypi.org/project/appdirs/) предоставляет переносимый способ:

```python
import appdirs   # $ pip install appdirs
user_data_dir = appdirs.user_data_dir("Название приложения", "Кто создал")
```

Разные платформы (Windows, MacOS, Linux) используют разные соглашения, `appdirs` позволяет не плодить сущностей и использовать на каждой платформе подходящие директории.


Links
-----

- [https://ru.stackoverflow.com/questions/535318/...](https://ru.stackoverflow.com/questions/535318/%D0%A2%D0%B5%D0%BA%D1%83%D1%89%D0%B0%D1%8F-%D0%B4%D0%B8%D1%80%D0%B5%D0%BA%D1%82%D0%BE%D1%80%D0%B8%D1%8F-%D0%B2-python)
- https://stackoverflow.com/questions/3718657/how-to-properly-determine-current-script-directory
