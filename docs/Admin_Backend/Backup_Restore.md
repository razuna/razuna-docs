**Backup & Restore or migrate from one database to another**

> *This option is available as of Razuna 1.4 and the new Razuna format as of Razuna 1.4.2!*

You have the option to backup & restore the complete Razuna database. This option will not only allow you to restore your complete Razuna server, but also migrate between different databases (say from MySQL to Oracle or MSSQL) with ease.

> The SQL and XML export are only for exporting your data. If you need to save a current state or migrate from one Razuna to another then you need to use the "Razuna format" option! This option does NOT backup your assets on your file system. It creates a restore point of your database records. You are solely responsible for your assets on the file system.

___

**Backup Razuna Server**

In order to backup your complete Razuna database and all settings you have to navigate to the Razuna Administration (usually located at [http://mydomain.com/razuna/admin](http://mydomain.com/razuna/admin)). Navigate to "System Settings" and then to "Backup & Restore".

Within the "Backup & Restore" tab you will then have the option to backup you Razuna server. Click on the "Backup" Button to conduct a backup. 

![](/Admin_Backend/img/Backup.jpg)

This will backup your whole database to a internal database which you can then use to import with the Restore option.

___

**Restore Razuna Server**

In case something is wrong with your Razuna Server or you migrated to a new one or you migrated to another database (say from H2 to MySQL, Oracle or MS SQL) you can simply restore the complete Server Backup file to your new Razuna server.

The current restore points are listed, with the latest restore point first. Click on the Restore link in order to restore to this point.

![](/Admin_Backend/img/Restore.jpg)

After the restore you might have to rebuild the search index of each host in order to avoid finding assets that are not in the current restore point. Also, you should check the "Log" directory of Razuna (located at "razuna/WEB-INF/bluedragon/work/cflog"). You will find a log file with the current date and time stamp. Errors with duplicate key or alike can be ignored!



