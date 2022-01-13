# MySQL. Выборка отсутствующих значений в одной из двух таблиц данных

```
mysql> SELECT COUNT(agrelink.iid) FROM agrelink LEFT JOIN item ON (agrelink.iid=item.id) WHERE item.id IS NULL;
+---------------------+
| COUNT(agrelink.iid) |
+---------------------+
|              231635 |
+---------------------+
1 row in set (12.03 sec)

mysql> select count(*) from item;
+----------+
| count(*) |
+----------+
|   668470 |
+----------+
1 row in set (0.00 sec)

mysql> select count(*) from agrelink;
+----------+
| count(*) |
+----------+
|   900105 |
+----------+
1 row in set (0.00 sec)
```

`900105 - 668470 = 231635`

Назад на [MySQL](:mysql)
