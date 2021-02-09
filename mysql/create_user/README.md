# Приклад створення БД, та користувача

Заходимо під root'ом в MySQL (MariaDB):

{% include cl.htm cmd="sudo mysql -uroot -p"
small="[sudo] password for olex: 
Enter password: 
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 47
Server version: 10.1.47-MariaDB-0ubuntu0.18.04.1 Ubuntu 18.04
..." %}

Дивимося, які бази є:

{% include cl.htm cmd="MariaDB [(none)]» show databases;"
small="
+--------------------+
| Database           |
+--------------------+
| autodb             |
| information_schema |
| library            |
| mysql              |
| performance_schema |
| swimdb             |
+--------------------+" %}


Створюємо нову базу даних:

{% include cl.htm cmd="MariaDB [(none)]» create database kazkadb;" %}


Створюємо користувача для web-інтерфейсу, встановлюємо йому пароль:

{% include cl.htm cmd="MariaDB [(none)]» CREATE USER 'kazka_user'@'localhost' IDENTIFIED BY 'PASSW_4_kazka_user';" %}

Надаємо користувачу мінімальні права для таблиць бази:

{% include cl.htm cmd="MariaDB [(none)]» GRANT SELECT, INSERT, UPDATE, DELETE ON kazkadb.* TO 'kazka_user'@'localhost';"
MariaDB [(none)]» FLUSH PRIVILEGES;" %}

---

## Создание пользователя одновременно с предоставляемыми правами

https://www.dmosk.ru/miniinstruktions.php?mini=mysql-user

Эта команда предоставляет права доступа пользователю и, если его не существует, создает его:

```mysql
GRANT ALL PRIVILEGES ON *.* TO 'dbuser'@'localhost' IDENTIFIED BY 'password' WITH GRANT OPTION;
```

Описание команды:

**ALL PRIVILEGES:** предоставляет полные права на использование данных.
** *.* :** права предоставляются на все базы и все таблицы.
**dbuser:** имя учетной записи.
**localhost:** доступ для учетной записи будет предоставлен только с локального компьютера.
**password:** пароль, который будет задан пользователю.
**WITH GRANT OPTION:** будут предоставлены дополнительные права на изменение структуры баз и таблиц.

## Другие примеры

Предоставление особых прав пользователю:

```mysql
GRANT SELECT, UPDATE ON base1.* TO 'dbuser'@'localhost' IDENTIFIED BY 'password';
```

* права на выборку и обновление данных во всех таблицах базы **base1 **для пользователя **dbuser**
* список всех возможных прав: all privileges, alter, create, create temporary tables, delete, drop, execute, file, index, insert, lock tables, process, references, reload, replication client, replication slave, select, show databases, shutdown, super, update, usage

Разрешение на удаленное подключение и использование базы MySQL:

```mysql
GRANT ALL PRIVILEGES ON *.* TO 'dbuser'@'192.168.0.55' IDENTIFIED BY 'password'
```

предоставит права пользователю **dbuser**, который будет подключаться с компьютера с IP-адресом **192.168.0.55.**

Создание учетной записи MySQL с правами создания резервных копий:

```mysql
GRANT SELECT, SHOW VIEW, RELOAD, REPLICATION CLIENT, EVENT, TRIGGER, LOCK TABLES ON *.* TO 'backup'@'localhost' IDENTIFIED BY 'backup';
```

## Возможные ошибки

**ERROR 1819 (HY000): Your password does not satisfy the current policy requirements**

Причина: в новых версиях по умолчанию активированы политики на проверку сложности пароля. Их список можно посмотреть командой:

```mysql
SHOW VARIABLES LIKE 'validate_password%';
```
Вывод команды будет, примерно, следующим:


| Variable_name                        | Value  |
| validate_password_check_user_name    | OFF    |
| validate_password_dictionary_file    |        |
| validate_password_length             | 8      |
| validate_password_mixed_case_count   | 1      |
| validate_password_number_count       | 1      |
| validate_password_policy             | MEDIUM |
| validate_password_special_char_count | 1      |

где:

* **validate_password_check_user_name** - пароль не должен совпадать с именем пользователя.
* **validate_password_dictionary_file** - использовать специальный файл со словарем запрещенных паролей.
* **validate_password_length** - минимальная длина пароля.
* **validate_password_mixed_case_count** - сколько, как минимум, должно быть символов в малой и большой раскладках.
* **validate_password_number_count** - какое минимальное количество цифр использовать в пароле.
* **validate_password_policy** - позволяет задать определенный набор правил. Доступны значения LOW (или 0), MEDIUM (1), STRONG (2).
* **validate_password_special_char_count** - минимальное количество специальных символов (например, # или !).

Решение:

* Привести пароль в соответствие требованиям политик.
* Отключить политику, которая не позволяет использовать желаемый пароль. Например, чтобы отключить требование использовать цифры вводим:

```mysql
SET GLOBAL validate_password_number_count = 0;
```

См. также: [Права для пользователей]({{ site.baseurl}}/mysql/privileges)
