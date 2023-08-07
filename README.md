# advanced-sql-part2
C:\xampp\mysql\bin>mysql.exe -u root
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 8
Server version: 10.4.24-MariaDB mariadb.org binary distribution

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> show databases;
+--------------------+
| Database           |
+--------------------+
| aaaa               |
| collage            |
| company            |
| info               |
| information_schema |
| mysql              |
| pavan              |
| performance_schema |
| phpmyadmin         |
| storesales         |
| student            |
| studentinfo        |
| test               |
| vishnu             |
+--------------------+
14 rows in set (0.074 sec)

MariaDB [(none)]> drop databases collage,company,info;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near 'databases collage,company,info' at line 1
MariaDB [(none)]> create database data;
Query OK, 1 row affected (0.073 sec)

MariaDB [(none)]> use data;
Database changed
MariaDB [data]> create table school(id int(10),name varchar(10),address varchar(10),birthyear int(4));
Query OK, 0 rows affected (0.189 sec)

MariaDB [data]> desc school;
+-----------+-------------+------+-----+---------+-------+
| Field     | Type        | Null | Key | Default | Extra |
+-----------+-------------+------+-----+---------+-------+
| id        | int(10)     | YES  |     | NULL    |       |
| name      | varchar(10) | YES  |     | NULL    |       |
| address   | varchar(10) | YES  |     | NULL    |       |
| birthyear | int(4)      | YES  |     | NULL    |       |
+-----------+-------------+------+-----+---------+-------+
4 rows in set (0.093 sec)

MariaDB [data]> insert table school values(411,'sai','telangana',2012);
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near 'table school values(411,'sai','telangana',2012)' at line 1
MariaDB [data]> insert school values(411,'sai','telangana',2012);
Query OK, 1 row affected (0.123 sec)

MariaDB [data]> insert school values(421,'hari','telangana',2013);
Query OK, 1 row affected (0.006 sec)

MariaDB [data]> insert school values(416,'lucky','andhra',2015);
Query OK, 1 row affected (0.006 sec)

MariaDB [data]> insert school values(426,'nanda','andhra',2015);
Query OK, 1 row affected (0.010 sec)

MariaDB [data]> select*from school;
+------+-------+-----------+-----------+
| id   | name  | address   | birthyear |
+------+-------+-----------+-----------+
|  411 | sai   | telangana |      2012 |
|  421 | hari  | telangana |      2013 |
|  416 | lucky | andhra    |      2015 |
|  426 | nanda | andhra    |      2015 |
+------+-------+-----------+-----------+
4 rows in set (0.034 sec)

MariaDB [data]> SELECT * FROM school WHERE id IN (SELECT id FROM school WHERE birthyear>2014);
+------+-------+---------+-----------+
| id   | name  | address | birthyear |
+------+-------+---------+-----------+
|  416 | lucky | andhra  |      2015 |
|  426 | nanda | andhra  |      2015 |
+------+-------+---------+-----------+
2 rows in set (0.080 sec)

MariaDB [data]> SELECT id, name,address, FROM school where birthyear < 2014;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near 'FROM school where birthyear < 2014' at line 1
MariaDB [data]> SELECT id, name,address FROM school where birthyear < 2014;
+------+------+-----------+
| id   | name | address   |
+------+------+-----------+
|  411 | sai  | telangana |
|  421 | hari | telangana |
+------+------+-----------+
2 rows in set (0.007 sec)

MariaDB [data]> SELECT * FROM school where address in (SELECT address FROM school WHERE address = 'andhra' );
+------+-------+---------+-----------+
| id   | name  | address | birthyear |
+------+-------+---------+-----------+
|  416 | lucky | andhra  |      2015 |
|  426 | nanda | andhra  |      2015 |
+------+-------+---------+-----------+
2 rows in set (0.099 sec)

MariaDB [data]> SELECT Name, id FROM school WHERE birthyear > (SELECT AVG( birthyear );
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near '' at line 1
MariaDB [data]> SELECT Name, id FROM school WHERE birthyear > (SELECT AVG( birthyear) );
Empty set (0.045 sec)

MariaDB [data]>
