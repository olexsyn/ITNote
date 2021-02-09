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

{% include cl.htm cmd="MariaDB [(none)]> show databases;"
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


https://www.dmosk.ru/miniinstruktions.php?mini=mysql-user

Эта команда предоставляет права доступа пользователю и, если его не существует, создает его:

```mysql
GRANT ALL PRIVILEGES ON *.* TO 'dbuser'@'localhost' IDENTIFIED BY 'password' WITH GRANT OPTION;
```

Описание команды:

**ALL PRIVILEGES:** предоставляет полные права на использование данных.
__ *.* :__ права предоставляются на все базы и все таблицы.
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
