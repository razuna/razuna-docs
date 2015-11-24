**Setup MSSQL Server for Razuna**

These step by step guides below will show you how one can setup a Razuna database and user within MS SQL Server. The screenshot have been taken from the MS SQL 2008 installation and might vary with older versions.

 * Enable SQL Authentication
 * Allow connection over TCP/IP
 * Setup a "Razuna" database
 * Setup a "Razuna" User
 * Add the "Razuna" Schema
 * Add permissions for the user "Razuna" to the database
 * Configure the "User Mapping" for the Razuna user

___

**Enable SQL Authentication**

By default MS SQL Server enables only Windows Authentication. In order for Razuna to connect successfully to the MS SQL Server you will need to enable SQL Server Authentication (or mixed mode). To do so, you need to open the "Server Properties" and navigate to "Security". On the right side chose "SQL Server and Windows Authentication mode".

![](/db_connect/img/mssqlauth.png)

___

**Allow connection over TCP/IP**

By default, all MSSQL Database server do not allow connection over TCP/IP. You will need to enable this in order for Razuna to connect to your MSSQL database. Go to the MSSQL Server Network interface and click ont he TCP/IP setting to enable it.

___

**Setup a "Razuna" database**

Setup a "Razuna" database by right clicking on the "Database" icon and then "New Database...". Name the database "razuna". Further configurations like permissions will be done later.

![](/db_connect/img/mssql-db-1.png)

![](/db_connect/img/mssql-db-2.png)

___

**Setup a "Razuna" User**

Add a new user by right clicking on the "Security" icon, then "New" and "Login..." (or expanding the Secuirity tree and then right clicking on "Logins") this will open a new window. Enter the user name "razuna" and hit ok to close the window. Further configuration will be done later on.

![](/db_connect/img/mssql-user-1.png)

![](/db_connect/img//mssql-user-2.png)

![](/db_connect/img/user-mapping.png)

___

**Add the "Razuna" Schema**

Since we place all of the Razuna databases in a schema we have to create a schema first. To do so, go to the Database tree, expand it and and right click on the "Security" Icon and chose "New" and then "Schema". Name the schema "razuna" and chose the user "razuna" as the owner of the schema.

![](/db_connect/img/mssql-schema-1.png)

![](/db_connect/img/mssql-schema-2.png)

___

**Add permissions for the user "Razuna" to the database**

Open the Properties for the Razuna database and add the user "razuna" to Permissions in order for the user to connect to the Razuna database. Click on the "search" button to enter the user. Make sure that the "Connect" permission is checked!

![](/db_connect/img/mssql-db-3.png)

___

**Configure the "User Mapping" for the Razuna user**

Last, we need to assign the database and the schema to the "razuna" user. To do so, expand the Security tree and expand the "Logins". Within you should see the "razuna" user. Open the Properties window and on the left side navigate to "User Mapping". On the right side, you should see all the available databases. Check the "razuna" one and add "razuna" as the default schema. In the bottom window make sure that there is also "db_owner" checked for this user.

![](/db_connect/img/mssql-user-3.png)




