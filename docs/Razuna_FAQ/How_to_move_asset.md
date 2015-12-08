**How to move the asset directory**

By default you will find the default folder for storing your assets in the web root of Razuna. That is to say it is NOT in the web root your DAM web application of WEB application. It is located in the root folder of the Razuna application.

For security reasons you might want to move this folder out of your web root or want to locate it on a shared drive, Amazon S3 or network volume. Also, when you use domain locater (DNS record) like [http://ourdam.mydomain.com](http://ourdam.mydomain.com/) to point to your DAM application you will need to create a virtual directory.

Creating a virtual directory within Tomcat (the default standalone web server for Razuna) is easy. First of locate the file "server.xml" in the Tomcat/conf folder. Open it in a text editor.

Then look for the <host> container. If you have not changed the default installation this is the "localhost" entry. In between the <host></host> container add the following;

```
<Context path="/assets" docBase="absolutepathtodirectory" crossContext="false" debug="0" reloadable="false" />
```

> **Important to know** : Please note, that when you call your Razuna installation with [http://localhost:8080/razuna](http://localhost:8080/razuna) then your asset path will be "/razuna/assets"! Also, the "docBase" should point to the directory you moved the "assets folder". This is a absolute path, on windows this should be "C:\....." on Linux/MacOS X "/....". Network paths on Windows have to be used as "//10.0.0.10/razuna/assets/" (enter your own ip of course)

Furthermore you need to adjust the path to the new asset directory in Razuna. Log on to the Razuna Administration and set the asset path for your host. Since each host can have a different asset path you have to change this per host. You will find the setting in the "General Settings / Digital Asset Management" view. Please refer to the screen shot.

![](/Razuna_FAQ/img/razuna-path.png)





