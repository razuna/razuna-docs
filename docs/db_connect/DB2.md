**DB2**

> **As of Razuna 1.6.2 we have stopped supporting the DB2 database!**

___

**How to setup DB2 with Razuna**

In this guide we assume that you got a working DB2 Server up and running or just installed one. If not, then please consult your administrator.

> **DB2 Editions** : Razuna works with all version of DB2 from version 9.5 on.

*Razuna will setup all the required tables for a successful Razuna deployment within the schema you enter during setup. We recommend that you setup the database with the following parameters:*

```
CREATE DATABASE razuna AUTOMATIC STORAGE YES USING CODESET UTF-8 COLLATE USING SYSTEM PAGESIZE 32768;
```

