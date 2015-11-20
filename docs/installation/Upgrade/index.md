**Upgrading Razuna**

*This page describes the recommended method of upgrading Razuna. With this method, you set up a new instance of Razuna, back up your data as an SQL or XML file from your existing Razuna instance, move over your hosts, and then restore that data into the new Razuna instance. The new Razuna will create the database structure (tables and indexes) before importing the data.*

> *These instructions also apply to moving Razuna from one server to another server.*

___

**Before you begin**

* Read the [release notes for the version you are upgrading to](http://wiki.razuna.com/display/ecp/Razuna+Release+Notes) and this **complete upgrade guide** for the version you are upgrading to, as there may be version-specific instructions.

* Double check the [Razuna Release Notes](http://wiki.razuna.com/display/ecp/Razuna+Release+Notes) that you don't need to run the "Update & Export Script" or that you have to run it!

* Check for known issues in the [Razuna Issue tracking platform](http://issues.razuna.com/).

* Test first! We strongly recommend that you carry out all of the following upgrade instructions in a test environment first. Do not upgrade your production Razuna until you are satisfied that the upgrade has been successful in your test environment.

If you have any problems with your test upgrade that you cannot resolve, create a support case in [http://issues.razuna.com](http://issues.razuna.com/) so that we can assist you.

If you have any problems during the upgrade of your production Razuna, do not allow your users to start using the new (upgraded) instance. Instead continue to use your old instance. This will help ensure that you do not lose production data. Create a support case in [http://issues.razuna.com](http://issues.razuna.com/) so that we can help you resolve the problems with the upgrade.

___

**Set up a new instance of Razuna**

Install the new version of Razuna

*You will need to set up a new instance of Razuna that you can migrate your existing data into. This involves installing a new empty instance of the desired version of Razuna and applying configuration changes to match the configuration of your old instance of Razuna.*

*Download and unpackage the Razuna distribution you require, to a new directory. Do not overwrite your old Razuna instance. Follow the installation instructions, either:*

* Installing Razuna Standalone (recommended), or

* [Installing Razuna WAR](/installation/WAR/) (note: if you are running WAR, read the latest instructions for your application server and perform any necessary configuration steps. E.g. If your application server needs extra libraries to run Razuna, the extra libraries currently in your application server for the old Razuna may be outdated. Make sure you get the extra libraries needed for your new version of Razuna.)

**Create a new empty database or schema**

*For example, if you are using a database 'razuna' with your existing installation, and you are upgrading to Razuna 1.4.1, create database or schema 'razuna_new' with identical access permissions. Consult your database administrator if you need assistance with this.*

*(Note: you do not need to create a new database if you are using the embedded database (H2)).*

*Follow the instructions for your preferred database:*

 * [Instruction for MySQL](/db_connect/MySQL/)
 * [Instruction for MS SQL](/db_connect/MSSQL)
 * [Instruction for Oracle](/db_connect/Oracle)
 * [Instruction for DB2](/db_connect/DB2)

**Configure your new Razuna instance**

* **Memory Settings** - You will most probably apply your recent memory settings to the new instance. In case you need help, consult our memory guidelines: [Adjusting Memory Settings for Tomcat](http://wiki.razuna.com/display/ecp/Adjusting+Memory+Settings+for+Tomcat) and [Configure Tomcat for production deployment](http://wiki.razuna.com/display/ecp/Configure+Tomcat+for+production+deployment).

* **Running Razuna on another port** - if your new instance of Razuna is installed on the same machine as your old Razuna, make sure it is running on a different port. For Razuna Standalone, refer to [Running Razuna on a different port](http://wiki.razuna.com/display/ecp/Running+Razuna+on+a+different+port). For Razuna WAR, consult your application server documentation.

**Startup Razuna**

Start the new Razuna instance server and run the First Time wizard. During the First Time Wizard you make sure that your new instance can connect to your database correctly and that the new instance performs as configured.

___

**Migrate your existing Razuna data to the new Razuna instance**

**Ensure that no users can access Razuna during migration**

You need to ensure that users cannot update your existing Razuna instance while you perform the migration, so that your backup will not contain inconsistent data.

*There are two ways to ensure that users cannot update your existing Razuna instance:*

* *Make Razuna inaccessible: Shut down Razuna, start it on a different port to the one that Razuna usually runs on and do the backup there. Please note, no-one will be able to access Razuna while it is running on a different port during the backup; or,*

* *Make Razuna read-only: In your database, remove 'write' permissions from the database user that Razuna uses. If you do this, users will be able to read assets but will not be able to update them during the backup.*

Leave your existing Razuna inaccessible or read-only until the upgrade is completed successfully.

**Create a backup of your current database**

**For Razuna 1.4.2 and later**

Using the backup option you can create a storage point for restoring into your new Razuna instance. Go to the Razuna Administration (usually located at [http://mydomain.com/razuna/admin](http://mydomain.com/razuna/admin)). Navigate to "System Settings" and then to "Backup & Restore".

Within the "Backup & Restore" tab you will then have the option to backup you Razuna server. Click on the "Backup" Button to conduct a backup.

![](/installation/img/Razuna_-_backup.jpg)

By clicking on Backup a new window will open showing you the progress of the backup.

**For Razuna up until version 1.4**

You should have a backup done already during executing the "Update & Export Script". If not then please read the Release Notes and follow the instructions there.

**Stop the Razuna Server**

Shutdown your Razuna server now, BEFORE going any further. This ensures that your old Razuna instance closes the database properly and that no one can access your assets anymore.

**Copy your backup to the new Razuna instance**

In order for your Backup to be recognized during the first time wizard or for a restore within the Razuna Administration you need to place the before mentioned Razuna Backup to the Backup folder of your new Razuna instance.

To do so, move the "razuna_backup.h2.db", "razuna_backup.trace.db" and the folder "razuna_backup.lobs" to the "/razuna/admin/backup" folder of the new Razuna instance. (Make sure that your new Razuna instance is shutdown)

**Move your "assets" folder**

If you have your "assets" folder inside your old Razuna instance you should also move your assets folder to the new Razuna instance. Simply copy the "assets" folder to the new Razuna instance (and by doing so overwriting the existing "assets" folder of the new Razuna instance).

**Move your hosts folders to the new Razuna instance**

Razuna creates for each host a "raz(id)" folder in your Razuna root folder. Copy each of these folders over to the Razuna root folder of the new instance. These folders might also contain customizations you have made to individual hosts.

**Start your new Razuna instance**

The final step of upgrading your Razuna is to start your new Razuna instance and import the data from your old Razuna instance.

* If you haven't already done so, shut down your old Razuna instance by stopping the Razuna server.

* If you are using Tomcat with your installation of Razuna (note: Razuna Standalone ships with Tomcat by default), delete the Tomcat work directory before restarting Razuna. If you do not do this, users may encounter errors when they try to display assets.

* Start up your new instance of Razuna.

**Import your old data to your new Razuna instance**

After you have successfully started your new Razuna instance, you will need to import the data from your old instance into the new instance.

There are 2 ways to import your backup data;

* Import your data during the first time wizard.

* Import your data after you have gone trough the first time wizard [within the Razuna Administration](http://wiki.razuna.com/pages/viewpage.action?pageId=13238290).

**Activate Host Settings**

Activate the recent changes to each host. Follow "[Activate hosts with new settings](http://wiki.razuna.com/display/ecp/Activate+hosts+with+new+settings)"

___

**Post-startup checks and tasks**

It is strongly recommended that you perform the following checks and tasks after you have started your new instance of Razuna:

Check your server logs for error messages, even if Razuna appears to be running correctly. If there are any errors there that you cannot resolve, create a support case in [http://issues.razuna.com](http://issues.razuna.com/), attach your log file and we will advise you on the errors.

* If you changed machines when upgrading or changed the paths to the Razuna root folder then you need to adjust the path in the "bluedragon.xml" file to the cfcollection.

* If you migrated any customisations from your old Razuna to the new Razuna, ensure that they are tested thoroughly.

**Congratulations! You have completed your upgrade of Razuna!**

___

**Troubleshooting**

* Check for known issues in the [Razuna Issue Tracker](http://issues.razuna.com/).

* If the upgrade fails for any reason, revert to using your old Razuna. Create a support case in [http://issues.razuna.com](http://issues.razuna.com/) and attach your log file, so that we can help you resolve the problems with the upgrade.

___

**Version Upgrades up until version 1.4**

 * [Upgrade from 1.3.5 to 1.4](/installation/upgrade/Upgrade from 135 to 14/)
 * [Upgrade from 1.2.3 to 1.3.5](/installation/upgrade/Upgrade from 123 to 135/)
 * [Upgrade from 1.2.3 to 1.3](/installation/upgrade/Upgrade from 123 to 13/)
 * [Upgrade from 1.2.2 to 1.2.3](/installation/upgrade/Upgrade from 122 to 123/)
 * [Upgrade from 1.2.1 to 1.2.2](/installation/upgrade/Upgrade from 121 to 122/)
 * [Upgrade from 1.2 to 1.2.1](/installation/upgrade/Upgrade from 12 to 121/)
 * [Upgrade from 1.1.4 to 1.2](/installation/upgrade/Upgrade from 114 to 12/)
 * [Upgrade from 1.1.3 to 1.1.4](/installation/upgrade/Upgrade from 113 to 114/)













