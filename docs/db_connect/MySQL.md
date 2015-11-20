**How to setup MySQL with Razuna**

In this guide we assume that you got a working MySQL Server up and running or just installed one. If not, then please consult your administrator or [download and install the MySQL Server](http://www.mysql.com/).

> **Important:** Make sure you create a database called "**razuna**" with a correct user and password that allows access to the database. Furthermore, tables need to be configured to use the high performance InnoDB storage system!

*Create the Razuna database with the following command:*

```
create database razuna character set utf8;
```

*For MySQL versions 5.6 and above the following global parameters also need to be set:*

```
SET GLOBAL innodb_large_prefix = 1;
SET GLOBAL innodb_file_format = barracuda;
SET GLOBAL innodb_file_per_table = true;
```

> **MySQL Versions** : Razuna has been tested with MySQL 4.x and 5.x

Razuna will setup all the required tables for a successful Razuna deployment within the "Razuna" database. Furthermore tables need to be configured to use the high performance InnoDB storage system. Please consult the page [Recommended MySQL settings](/db_connect/Recommended MySQL settings/) for the recommended MySQL setup for Razuna.


We still recommend that you take a look at our [Recommended MySQL settings](/db_connect/Recommended MySQL settings/).
