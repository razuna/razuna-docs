**Installation Trouble-Shooting**

**Java based problems**

First make sure that the JAVA_HOME variable must be set correctly to your Java installation. You should install the JDK.

If you see this error on server startup:
ERROR [protocol] FTP Socket error
java.net.BindException: Address already in use: JVM_Bind at java.net.PlainSocketImpl.socketBind(Native Method)
Check to see if you have any services running against port 8080

___

**Images and Videos don't show**

The following steps should help you pinpoint the problem why Images and Videos don't show within Razuna.

1. Check that ImageMagick works
Upload an image to Razuna and then check the directory "/razuna/demo/dam/incoming" for any folders (you can remove all folders first in order to see the new folder). If there is the image and a xxx_thumb.jpg file AND you can view the thumb file in the image viewer then it works.

2. Check your asset path
The new image from above should haven been moved to the "/razuna/assets" folder. Check in that folder that the image is really there. If this is your test system and you only have one host your structure will be something like "/razuna/assets/1(hostid)/3(folderid)/img/(imageid)".

If the image and thumb is in the assets path then let's check the settings in Razuna.

3. Check settings in Razuna
Go to the Razuna Administration (http://localhost:8080/razuna/admin) and then to Settings/Global Settings. In the DAM tab check that the path to the assets folder is set correctly.

If the path is correct, but images still don't show, continue...

4. Check that the context path exists
Open the file server.xml, which can be found in "/tomcat/conf/". Scroll all the way to the bottom and check that the localhost contains the line:

```
<Context path="/assets" docBase="/razuna/assets/" crossContext="false" reloadable="true" />
```

If you deploy Razuna on a Ubuntu Or Debian based Linux system you will need to change the path to the "assets" folder within the server.xml file to an absolute path.

```
<Context path="/assets" docBase="/opt/razuna_tomcat_1_1_4/tomcat/webapps/razuna/assets/" crossContext="false" reloadable="true" />
```

If you deploy on Windows with a NETWORK path you should use the "//ip/" path, like:

```
<Context path="/assets" docBase="//10.0.0.10/razuna/assets/" crossContext="false" reloadable="true" />
```

> **Word on the path** : Note: if your Razuna URL contains "[http://ip/RAZUNA/raz1....](http://ip/RAZUNA/raz1)" then you need to set the path above to path="/razuna/assets" !!!

___

**Problem with connecting to MS SQL database**

By default MS SQL database does **not** allow connections over TCP/IP. Select the network properties of the MS SQL Server and enable it in order for Razuna to connect to it properly.