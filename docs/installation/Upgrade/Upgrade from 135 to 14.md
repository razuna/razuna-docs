**Upgrade from 1.3.5 to 1.4**

**Overview**

Razuna 1.4 is a big point release and as such brings a set of new features and enhancements. You can lookup the release notes at the public Issue Tracker at [http://issues.razuna.com](http://issues.razuna.com).

> We have changed the Update procedure from Razuna 1.4 on forward. From now on, you simply export the data and import it to the new Razuna instance. To make your current 1.3.5 installation compatible with the new 1.4 structure we created a dedicated update script. You only need to apply this ONE TIME

___

**Update Procedure**

You should always make a backup or Razuna and especially of your database before attempting any update! That said, this process of updating Razuna is quite simple.

* Grab the Update Script
* Run the Update
* Install Razuna 1.4
* Run the first time wizard and import your data
* Re-create your hosts

___

**Grab the update script**

The update scripts are available at two places:

* In the Razuna 1.4 download: The "export" directory in the root directory of Razuna.

* Download separately: [Click here to download the update scripts from our servers](http://s.razuna.com.s3.amazonaws.com/installers/update_1.3.5/export.zip).

Once you have the export directory, simply copy it to your Razuna 1.3.5 root directory.

___

**Run the Update**

Updating Razuna 1.3.5 to the new Razuna 1.4 structure involves two steps. First you need to update your database and then create a export file that will be used to import into Razuna 1.4.

Go to the Update script page with the following URL: http://(domain)/(razuna)/export. Where (domain) should be your domain with port. Depending on your server setup you either need to pass the razuna part or not. For most users the URL probably is: [http://localhost:8080/razuna/export](http://localhost:8080/razuna/export).

**Update database**

On the Update script page click on the "Update Database" Button to update your Razuna 1.3.5 database.

![](/installation/img/update-1.png)

**Create the Export file**

Now that your database is updated you can export your data. This script will create a XML file which you can then use to import to your new Razuna 1.4 installation.

Click on the "Create Backup file" Button. A new window will open and show the process of your backup. At the end of the process you can then either click on the link to download the Backup file to your desktop. The backup file will be also available in the "backup" directory of the "export" directory. This is the file that we will be using for importing to Razuna 1.4.

![](/installation/img/update-2.png)

You can now safely close your browser and shut down the Razuna server.

___

**Install Razuna 1.4**

If you haven't done so, you should now grab your copy of Razuna 1.4 and install it on your server. Follow the below steps for the proper migration from Razuna 1.3.5 to 1.4.

**Copy the "assets" folder**

Copy the "assets" folder from 1.3.5 to the 1.4 directory. Yes, this means overwriting the existing one.

**Install the latest ffmpeg application**

With Razuna 1.4 you are able to store and convert videos in the OGG and WebM format. In order for Razuna to work with those new formats you need to update your ffmpeg application the the latest version. You can find the new ffmpeg in the "applications" folder of your Razuna 1.4 download. If you are on MacOS X or Linux you should follow the guide in the Wiki (1. Install ImageMagick, Ghostscript, FFmpeg and Exiftool) for updating your ffmpeg installation. 

After installation, start the server as usual (make sure that Razuna 1.3.5 is shut down) and to to your Razuna website, usually [http://localhost:8080/razuna](http://localhost:8080/razuna). You will be presented with the new firsttime wizard.

___

**Run the first time wizard and import your data**

Razuna 1.4 features a new firsttime wizard. With it, you can choose your setup, what database you like to use and of course, import your backup file. Since we are upgrading from 1.3.5 the steps below outline the way to import your data.

**First screen**

When you are at the firttime wizard page you should select "Custom Installation". The custom installation allows you to choose your database and import your backup file.

![](/installation/img/ftw-1.png)

**Choose database setup**

In this step you have the option to install Razuna to your preferred database. You can either use the embedded database, MySQL, MS SQL, Oracle or DB2. If you are **not** using the embedded database then please make sure that you followed our database guide for Razuna ([Connecting Razuna to a database](/db_connect/)) **before** you continue. Once you made your choice, click on continue.

![](/installation/img/ftw-2.png)

**Choose to import file**

In this step you either have the option to continue with a new database setup or import your backup file. Obviously, we want to continue with importing our backup file.

![](/installation/img/ftw-3.png)

**Select backup file and import**

Here you can either upload your backup file or if you placed it in the Razuna 1.4 admin/backup directory it will show in the list below. Either way, once your backup file is available you can click on import. This will open a new window and will show you the progress of the import. Please be patient for larger datasets, since it can take some time to import.

![](/installation/img/ftw-4.png)

After clicking the "Import" Button a new window will show you the progress of the import. If all goes well, you can see the success message at the bottom of the window. close it when done successfully.

![](/installation/img/ftw-5.png)

After everything has been imported you should click on the "Razuna link" for being redirected to the usual Razuna login.

![](/installation/img/ftw-6.png)

___

**Re-create your hosts folders**

> If you have only one host (demo) then you can skip this step!

If you have more then one host, you have to re-create your hosts with the build in update function of Razuna. 

Log in to the Razuna Administration and navigate on the left side to the Menu "Customers/Domains/Hosts" and click on "List/add Hosts". Then click on the update icon for **each** host that you have in your list (see screenshot below). 

This will re-create your hosts folders and apply the latest updates. If you have made customization to any of those host folders in Razuna 1.3.5 you will need to copy over those changes to the new host folder. (Note: They are all called "raz(ID)" now! Where (ID) is the ID of the host which you can see in the host overview)

![](/installation/img/updatehosts.png)

___

**Post-startup checks and tasks**

 * Check your server logs for any error messages. You can also check the update logs for any problems during import.
 * Make sure that your assets are shown properly.
 * Upload a file of each asset type in order to check that the applications (ImageMagick, FFmpeg, etc.) still work as expected.
 * Generally test that everything behaves as it should.
 * Apply any server wide customizations to the new Razuna Tomcat instance.

If you have any errors or requests then please log them at our public tracker over at [http://issues.razuna.com](http://issues.razuna.com) or post a message on our Forums at [http://support.razuna.com](http://support.razuna.com). 

**Congratulations! You have completed your upgrade of Razuna.**





