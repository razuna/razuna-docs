**How to serve the DAM folder as its own web root**

**The Goal**

Many users would like to serve the "DAM" folder directly to the user when they call the domain [http://dam.razuna.com](http://dam.razuna.com) instead of having the user call the URL like [http://dam.razuna.com/razuna/mysite/dam](http://dam.razuna.com/razuna/mysite/dam).

___

**The Solution**

Since within the J2EE server "world" each web root is a application the prerequisite is to have the "bluedragon" and the "WEB-INF" folder within the root of the serving folder. Since we want to serve the "DAM" folder directly it becomes automatically the root folder for the Web Server, thus we need to have those two folders in the "DAM" folder.

___

**Configure the DAM folder**

In the Razuna root folder you will find the "bluedragon", "WEB-INF" and "global" folders. You will need to create a symbolic link to these folders when you want to server the DAM folder on its on.

On Linux/Unix you can issue the following command in the shell (do this within the DAM folder, e.g. raz1/dam):

```
ln -s /opt/tomcat/webapps/razuna/bluedragon bluedragon
ln -s /opt/tomcat/webapps/razuna/WEB-INF WEB-INF
ln -s /opt/tomcat/webapps/razuna/global global
```

Of course, you should be using the your path. Remember to use absolute paths!

For Windows there is no such thing as a symbolic link, but there is Junction. Junction allows you to do the same as symbolic links. You can download and see how to use junction over at [http://technet.microsoft.com/en-us/sysinternals/bb896768.aspx](http://technet.microsoft.com/en-us/sysinternals/bb896768.aspx). Do not create shortcuts as it will **not** work!

___

**Configure Tomcat**

The only thing left to do now is to configure Tomcat to serve your DAM folder directly. For this you will need to stop your Razuna server and open the server.xml file (this can be found within the tomcat/conf folder).

Locate the Host container (all the way to the bottom) and add/edit the Host in question. For our example, our new host entry looks like this:

```
<Host name="dam.razuna.com" appBase="webapps">
 <Context path="" docBase="/opt/tomcat/webapps/razuna/demo/dam/" allowLinking="true" />
 <Context path="/assets" docBase="/opt/tomcat/webapps/razuna/assets/" crossContext="false" reloadable="true" />
</Host>
```

It's important that the first "Context" contains the line "**allowLinking="true**"", without it our symbolic links would not work. Also make sure that the second "Context" is pointing to the exact location of your assets.

That's it. Simply startup your Razuna server and you should be able to server your DAM folder directly when you call up your host now.

