# MySQL

- [Типы данных](datatype)
  - [Про NULL](null)
- [ALTER TABLE](alter_table)
- [Как удобно посмотреть данные, когда строка вывода слишком широкая](wide_tables)
- [Примеры таблиц swimdb](swimdb)

## Приклад створення БД, та для користувача

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


Створюємо нову базу даних:

{% include cl.htm cmd="MariaDB [(none)]> create database kazkadb;" %}


Створюємо користувача для web-інтерфейсу, встановлюємо йому пароль:

{% include cl.htm cmd="MariaDB [(none)]> CREATE USER 'kazka_user'@'localhost' IDENTIFIED BY 'PASSW_4_kazka_user';" %}

Надаємо користувачу мінімальні права для таблиць бази:

{% include cl.htm cmd="MariaDB [(none)]> GRANT SELECT, INSERT, UPDATE, DELETE ON kazkadb.* TO 'kazka_user'@'localhost';"
MariaDB [(none)]> FLUSH PRIVILEGES;" %}


---

- Внешние ключи
  - [Внешние ключи](https://metanit.com/sql/mysql/2.5.php)
  - https://pro-prof.com/forums/topic/foreign-key-mysql
  - http://www.mysql.ru/docs/man/ANSI_diff_Foreign_Keys.html - плюсы и минусы
  - http://www.mysql.ru/docs/man/example-Foreign_keys.html - пример
  
- JOIN
  - https://andreyex.ru/bazy-dannyx/uchebnoe-posobie-po-sql/sql-operator-inner-joins/
  - https://andreyex.ru/bazy-dannyx/uchebnoe-posobie-po-sql/sql-operator-left-join/
  - https://andreyex.ru/bazy-dannyx/uchebnoe-posobie-po-sql/sql-operator-right-joins/
  - https://andreyex.ru/bazy-dannyx/uchebnoe-posobie-po-sql/sql-operator-full-joins/
  - https://andreyex.ru/bazy-dannyx/uchebnoe-posobie-po-sql/sql-operator-self-joins/
  - https://andreyex.ru/bazy-dannyx/uchebnoe-posobie-po-sql/sql-cartesian-ili-cross-joins/
  

https://andreyex.ru/bazy-dannyx/bd-mysql/vnutrennee-soedinenie-mysql/

https://andreyex.ru/bazy-dannyx/uchebnoe-posobie-po-sql/sql-strokovye-funkcii/

https://andreyex.ru/bazy-dannyx/uchebnoe-posobie-po-sql/sql-chislovye-funkcii/

https://andreyex.ru/bazy-dannyx/10-rasprostranennyh-oshibok-programmirovaniya-na-sql-i-kak-ih-izbezhat/

https://andreyex.ru/bazy-dannyx/baza-dannyx-mysql/11-osnovnyx-primerov-komandy-update-v-mysql/

https://andreyex.ru/mysql/peremennye-mysql/ + https://andreyex.ru/mysql/peremennaya-select-into-v-mysql/

https://andreyex.ru/mysql/vybor-sluchajnyh-zapisej-v-mysql/

https://andreyex.ru/mysql/kak-sbrasyvat-znacheniya-avtoinkrementa-v-mysql/

https://andreyex.ru/mysql/mariadb-protiv-mysql/

https://andreyex.ru/mysql/kak-sopostavit-znacheniya-null-s-drugimi-znachimymi-znacheniyami/

https://andreyex.ru/mysql/mysql-kommentarii-v-glubinu/



[MariaDB Connector/Python](https://mariadb.com/docs/appdev/connector-python/)

[Как установить PostgreSQL на Ubuntu 20.04](https://andreyex.ru/ubuntu/kak-ustanovit-postgresql-na-ubuntu-20-04/)
