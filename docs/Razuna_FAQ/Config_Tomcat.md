**Configure Tomcat for production deployment**

Tomcat is a great J2EE server and runs thousands of sites on the net. Unfortunately, there are no hard rules to adjust for "the best" production deployment settings, but here are the settings that worked the best in our experience with Razuna and Tomcat.

___

**Use a front end web server**

Thought, Tomcat can be used to serve Razuna directly, we encourage the use of a front end web server like IIS (best), Apache (better) or Nginx (the best). We have written dedicated pages how to do this with [Apache](/Razuna_FAQ/Razuna_Apache2/) and [Nginx](/Razuna_FAQ/Razuna_Nginx/).

___

**Memory & Garbage Collection Settings**

We already have a [dedicated site for Tomcat memory setting](/Razuna_FAQ/Adjust_memory/), but for production environment you should set the Maximum Heap Space to around 60% of your total RAM. The rule is to use as less as possible.

So, say you have 4GB of total RAM your memory settings would be (with a 60% rule and a bit less):

```
CATALINA_OPTS="-server -Xss1G -Xms2G -Xmx2G -XX:NewSize=1G -Xincgc $CATALINA_OPTS"
```

___

**Tomcat APR**

For optimal performance configuring and installing APR for Tomcat is a absolute must. We encourage you to [read the installation note on the dedicated APR Tomcat site](http://tomcat.apache.org/tomcat-6.0-doc/apr.html).

___

**Tomcat Connector settings**

After many months of trial and error we have found the following connector setting do work the best with Razuna:

```
<Connector port="8080" protocol="HTTP/1.1"
               connectionTimeout="3000"
               redirectPort="8443"
               maxPostSize="0"
               maxThreads="200"
               enableLookups="false"
               disableUploadTimeout="false"
               maxKeepAliveRequests="-1"
               useBodyEncodingForURI="true"
               compression="on"
               server="Razuna Application Server"
               />
```

> Apache Tomcat by default sets a limit on the maximum size of HTTP POST requests it accepts. In Tomcat, this limit is set to 2 MB. When you try to upload files larger than 2 MB to Razuna, a error can occur.

> The solution is to reconfigure Tomcat to accept larger POST requests, either by increasing the limit, or by disabling it. This can be done by editing /razuna/tomcat/conf/server.xml. Set the Tomcat configuration parameter maxPostSize for the HTTPConnector to a larger value (in bytes) to increase the limit. Setting it to 0 in will disable the size check. See the Tomcat Configuration Reference for more information.([http://tomcat.apache.org/tomcat-7.0-doc/config/http.html](http://tomcat.apache.org/tomcat-7.0-doc/config/http.html))

