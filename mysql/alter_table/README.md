# ALTER TABLE

Оператор ALTER TABLE обеспечивает возможность изменять структуру существующей таблицы. Например, можно добавлять или удалять столбцы, создавать или уничтожать индексы или переименовывать столбцы либо саму таблицу. Можно также изменять комментарий для таблицы и ее тип.

Оператор ALTER TABLE во время работы создает временную копию исходной таблицы. Требуемое изменение выполняется на копии, затем исходная таблица удаляется, а новая переименовывается.

Например, чтобы **переименовать столбец** INTEGER из a в b, можно сделать следующее:

    mysql> ALTER TABLE t1 CHANGE a b INTEGER;

Если переименованный столбец был индексируемым - индекс тоже перестроится под новое имя.

При **изменении типа столбца**, но не его имени синтаксис выражения CHANGE все равно требует указания обоих имен столбца, даже если они одинаковы. Например:

    mysql> ALTER TABLE t1 CHANGE b b BIGINT NOT NULL;

Однако начиная с версии MySQL 3.22.16a можно также использовать выражение MODIFY для **изменения типа столбца без переименовывания** его:

    mysql> ALTER TABLE t1 MODIFY b BIGINT NOT NULL;


```
mysql> desc users;
+--------+------------------+------+-----+------------+----------------+
| Field  | Type             | Null | Key | Default    | Extra          |
+--------+------------------+------+-----+------------+----------------+
| uid    | int(10) unsigned | NO   | PRI | NULL       | auto_increment |
| umail  | varchar(50)      | NO   | UNI | NULL       |                |
| upass  | varchar(100)     | NO   |     | NULL       |                |
| uses   | varchar(50)      | NO   | MUL |            |                |
| ustime | date             | NO   |     | 2012-01-01 |                |
+--------+------------------+------+-----+------------+----------------+
5 rows in set (0.00 sec)

mysql> ALTER TABLE users MODIFY ustime DATETIME NOT NULL DEFAULT "2012-01-01 00:00:00";
Query OK, 0 rows affected (0.05 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc users;
+--------+------------------+------+-----+---------------------+----------------+
| Field  | Type             | Null | Key | Default             | Extra          |
+--------+------------------+------+-----+---------------------+----------------+
| uid    | int(10) unsigned | NO   | PRI | NULL                | auto_increment |
| umail  | varchar(50)      | NO   | UNI | NULL                |                |
| upass  | varchar(100)     | NO   |     | NULL                |                |
| uses   | varchar(50)      | NO   | MUL |                     |                |
| ustime | datetime         | NO   |     | 2012-01-01 00:00:00 |                |
+--------+------------------+------+-----+---------------------+----------------+
5 rows in set (0.00 sec)
```

## Примеры

Ниже приводятся примеры, показывающие некоторые случаи употребления команды ALTER TABLE. Пример начинается с таблицы t1, которая создается следующим образом:

    mysql> CREATE TABLE t1 (a INTEGER,b CHAR(10));

Для того чтобы **переименовать таблицу** из t1 в t2:

    mysql> ALTER TABLE t1 RENAME t2;

Для того чтобы **удалить столбец** c:

    mysql> ALTER TABLE t2 DROP COLUMN c;

Для того чтобы **добавить новый числовой столбец** AUTO_INCREMENT с именем col:

   mysql> ALTER TABLE t2 ADD col INT UNSIGNED NOT NULL AUTO_INCREMENT, ADD INDEX (c);

Заметьте, что столбец `col` индексируется (`ADD INDEX`), так как столбцы AUTO_INCREMENT должны быть индексированы, и, кроме того, не могут быть NULL. [Подробнее про NULL](/mysql/null/)

Для того чтобы **изменить тип столбца** с INTEGER на TINYINT NOT NULL (оставляя имя прежним) и **изменить тип столбца** b с CHAR(10) на CHAR(20) **с переименованием** его с b на c:

```sql
ALTER TABLE t2 MODIFY a TINYINT NOT NULL, CHANGE b c CHAR(20);
```

Для того чтобы **добавить новый столбец** TIMESTAMP **в конец таблицы** с именем d:

    mysql> ALTER TABLE t2 ADD d TIMESTAMP;

Вставить новый **столбец после указанного столбца**:

    mysql> ALTER TABLE contacts ADD email VARCHAR(60) AFTER name;

Вставить новый **столбец в начало таблицы**:

    mysql> ALTER TABLE contacts ADD email VARCHAR(60) FIRST;

Для того чтобы **добавить индекс к столбцу** d и сделать столбец a первичным ключом:

    mysql> ALTER TABLE t2 ADD INDEX (d), ADD PRIMARY KEY (a);

**создать индексы** к таблице

    mysql> ALTER TABLE tmptab ADD FULLTEXT INDEX `idx_goods` (`goods`), ADD INDEX `idx_price` (`price`);

    mysql> ALTER TABLE swr ADD UNIQUE INDEX uni_name_year (lname, fname, year);

**удалить индекс**

    mysql> alter table vendor drop index idx_name;

## См. также

[Как посмотреть все индексы таблицы](mysql:show_index)

