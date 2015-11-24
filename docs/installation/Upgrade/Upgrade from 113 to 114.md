**Upgrade from 1.1.3 to 1.1.4**

**Overview**

Thought, Razuna 1.1.4 is only a small feature set release, it is a great stepping stone to Razuna 1.2. So, here are the changes for 1.1.4;

**Folder Permissions**

A folder can now be owned by a user only. Previously, you had to share a folder with the "Everyone" group. Now, you can simply uncheck the "Everyone" group and the folder will only be accessible to you. Others will not see the folder and all assets within are protected. Also, assets can not be found with the search once they are in a user protected folder. We also fixed an issue with inheritance of folder permissions.

**Internet Explorer Compatible**

It's not always easy to develop for all platforms and all browsers alike. Even thought we only use CSS and Javascript, there are sometimes browser platform issues that can not be overcome easily. Thus I am very happy to say that Razuna 1.1.4 is now compatible with IE 7 & 8. Whereas Razuna acts and looks much better with IE8 then IE7 (don't turn on Compatible mode, that thing makes it worse)...

**Performance, performance**

Due to a new version of the Application Server and its new feature to cache Javascript, CSS files and certain parts of Razuna, the new version is magnitudes faster. But we not only improved the loading of Razuna, but also streamlined our code much more. You can see an immediate effect of this new performance by uploading your assets. Assets are now uploaded in the back and you will be notified by eMail of the upload process, respectively when the assets has been uploaded to the server.

**Miscellaneous**

Our international users will be happy to see that Razuna can now search words with foreign characters (like German umlauts and Norwegian characters) correctly. You can now upload your own logo and it will be shown everywhere instead of the default Razuna logo. User timeouts are handled correctly and we made a couple of subtle design changes.

___

**Changes to the global configuration file**

With 1.1.4 we did a minimal change to the name of the cloud config parameter. Thus we kindly ask you to change the name from cloud to storage. See the below code;

From: 

```
<configid name="cloud">
 <thetext>local</thetext>
</configid>
```

To:

```
<configid name="storage">
 <thetext>local</thetext>
</configid>
```

**Additional config parameters added to 1.1.4.**

Please add the following additional configuration parameter:

```
<configid name="nirvanix_appkey">
 <thetext></thetext>
</configid>
<configid name="nirvanix_master_name">
 <thetext></thetext>
</configid>
<configid name="nirvanix_master_pass">
 <thetext></thetext>
</configid>
<configid name="nirvanix_url_services">
 <thetext>http://services.nirvanix.com</thetext>
</configid>
<configid name="isp">
 <thetext>false</thetext>
</configid>
```

___

**Upgrade path**

After you have installed Razuna 1.1.4 you should navigate to [http://yourdomain/admin/update.cfm](http://yourdomain/admin/update.cfm). This will check if there is an update needed for your database. If so, then please run the update before continuing working with version 1.1.4.

___

**Update Procedure**

You should always make a backup or Razuna and especially of your database before attempting any update! That said, this process of updating Razuna is quite simple.

* Download and unarchive the latest release.
* Stop the Razuna (or J2EE) server.
* For Windows Users only: Replace the new included FFMPEG application with your existing one! This version fixes some issues people had with converting videos to different formats.
* Copy the folders "admin" and "global" of the **new version** and drop them into your existing Razuna installation folder.
* Start the Razuna (or J2EE) server.
* Hit the usual Update URL at [http://localhost:8080/razuna/admin/update.cfm](http://localhost:8080/razuna/admin/update.cfm) to check if your database needs a update!
* Log in to the Razuna Administration and navigate to "Settings/List/add Hosts" then apply the update to each host that you have in your list.

* Your copy of Razuna is now updated and so are all hosts you have.
