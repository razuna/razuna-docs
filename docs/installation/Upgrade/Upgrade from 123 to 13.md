**Upgrade from 1.2.3 to 1.3**

> You can only update from Razuna 1.2.3 to Razuna 1.3!

___

**Overview**

Razuna 1.3 is another big point release and as such brings a set of new features and enhancements. The list below is only a short list of new features we added for 1.3. You can lookup the release notes at the public Issue Tracker at [http://issues.razuna.com](http://issues.razuna.com).

___

**Notable Changes**

 * MS SQL support. Tested with MS SQL 2005 and 2008.
 * Languages can now be en-/disabled.
 * Option to define your own extensions.
 * You are now able to download any asset directly.
 * You can upload your custom logo within the DAM administration.
 * Fully compatible with Internet Explorer 8.
 * Option to add assets to a collection from the list and search page.
 * Users are now able to create subfolders (previously only administrators could do that).
 * Many improvements to the Developer API among those a API for Collections and Users.

___

**Update Procedure**

You should always make a backup or Razuna and especially of your database before attempting any update! That said, this process of updating Razuna is quite simple.

 * Download and unarchive the latest release from [http://razuna.org/download](http://razuna.org/download).
 * Stop the Razuna (or J2EE) server.
 * Copy the folders "admin" and "global" of the new version and drop them into your existing Razuna installation folder.
 * Start the Razuna (or J2EE) server.

___

**Run the Update Script**

> *We have changed the way we store passwords and thus changed also the authentication. **Before** you can login to Razuna again, you need to run the Update procedure by going to [http://yourdomain/admin/update.cfm](http://yourdomain/admin/update.cfm) (depending on your installation your URL might contain "razuna" as in [http://yourdomain/razuna/admin/update.cfm](http://yourdomain/razuna/admin/update.cfm)).*

___

**Update your hosts**

Log in to the Razuna Administration and navigate to "Settings/List/add Hosts" then apply the update to each host that you have in your list

Your copy of Razuna is now updated and so are all hosts you have.

___

**Important Changes to your custom configuration**

This only applies to users who are using Oracle or MySQL with Razuna! 

Previously, if you are using your own database, such as Oracle or MySQL, you had to change the config.xml file. With Razuna 1.3 this is no longer needed as we are providing a user interface within the Razuna Administration for this. The update procedure (as described above) moved all your settings to an internal database. Please check that those settings are still in place and configure for your own environment. Navigate to the Razuna Administration and go to the new menu "System Settings". Especially, check the "Storage" and the "Database Settings".

![](/installation/img/admin.png)

___

**Update Razuna Desktop**

If you are using Razuna Desktop (you should really use it since it will make interactions with Razuna so easy) the you should immediately update your client installation with the latest release. The automatic update should have prompted you for that. If not, then please manually download the latest release from [http://razuna.org/download](http://razuna.org/download).

___

**Update FFMpeg, ImageMagick, Ghostscript and Exiftool**

In the download you will find the latest version of FFMpeg, ImageMagick, Ghostscript and Exiftool. Please update your copies to the recent versions since some features are only available in the latest releases, especially for FFMpeg. If you are on Linux or MacOS X you can simply update your local copies with the system utilities like port or yum. On Linux you probably have to recompile FFMpeg and ImageMagick. Please use our guide for that.

