**Razuna WAR Installation**

___

**Deploy the Razuna WAR on your J2EE server**

*The WAR/EAR distribution of Razuna is actually the same as the standalone server, just comes without the J2EE Server (obviously) and with the needed third party applications. Thus you will need to configure your server to work successfully with Razuna. Please find the needed additional steps below.*

___

**Configure your J2EE server configuration**

*Razuna stores all assets in a dedicated directory. Since this directory is usually stored outside of your webroot or on another hard drive (or even in the cloud) you will have to add a "Alias" to that folder in your localhost container.*

*As a example on Tomcat you can make use of the "Context" parameter to achieve this. This is done with the following line that should be put inside the localhost host container:*

```
<Context path="/assets" docBase="/razuna/assets/" crossContext="false" reloadable="true" />
```

> *On Ubuntu and Debian systems the **docBase** has to be a absolute path or else it will not work!*

*Remember this code is within the <host></host> container. If you are adding a new host you will need to copy this context path to each host you have!*

___

**Installing ImageMagick, FFmpeg and ExifTool**

*Depending on your operating system please refer to the following pages for the installation for the additional tools:*

* [Install Razuna on Linux](/installation/linux/)
* [Install Razuna on MacOS X](/installation/macosx/)
* [Install Razuna on Windows](/installation/windows/)