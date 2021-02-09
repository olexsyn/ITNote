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


Створюємо нову базу даних:

{% include cl.htm cmd="MariaDB [(none)]> create database kazkadb;" %}


Створюємо користувача для web-інтерфейсу, встановлюємо йому пароль:

{% include cl.htm cmd="MariaDB [(none)]> CREATE USER 'kazka_user'@'localhost' IDENTIFIED BY 'PASSW_4_kazka_user';" %}

Надаємо користувачу мінімальні права для таблиць бази:

{% include cl.htm cmd="MariaDB [(none)]> GRANT SELECT, INSERT, UPDATE, DELETE ON kazkadb.* TO 'kazka_user'@'localhost';"
MariaDB [(none)]> FLUSH PRIVILEGES;" %}

