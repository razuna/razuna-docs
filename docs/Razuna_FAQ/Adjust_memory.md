**Adjusting Memory Settings for Tomcat**

**Memory Settings for Tomcat**

Tomcat runs as a deamon under Linux or application/service on Windows. Depending on your setup and operating setup please find the instructions to set the memory for Tomcat.

By default, Tomcat sets its own memory size at around 64MB which by far this is not enough for web applications. You can set the "start size", the "maximum size" and you also need to up the heap space. to find out the proper values for your platform you will need to issue the command "java -X" in the terminal.

-Xms<size> set initial Java heap size
-Xmx<size> set maximum Java heap size
-Xss<size> set java thread stack size

Once you know your parameters you should allocate about 60% of your available Ram to Tomcat.

___

**Increase Memory**

**Linux**

To set the memory you should have a file called "setenv.sh" in your /tomcat/bin directory. If the file does not exsist you should create it. Within the file set the parameters like;

```
export JAVA_OPTS="-Xms256m -Xmx512m"
```
Then restart Tomcat to apply the new settings.

**Windows (started manually)**

To set the memory you should have a file called "setenv.bat" in your /tomcat/bin directory. If the file does not exsist you should create it. Within the file set the parameters like;

```
set JAVA_OPTS="-Xms256m -Xmx512m"
```

Then restart Tomcat to apply the new settings.

**Windows (as a service)**

If you are running Tomcat on a Windows server, then Tomcat should be installed as a service. Installing Tomcat as a service is really easy. Simply change to the "bin" directory of Tomcat and issue the following command:

```
service install
```

This will install Tomcat as a service. In order to configure the service itself there is another application in the "bin" directory called "Tomcat7w.exe". This will give you a GUI to configure all aspects of the service itself (like memory, etc.).

Tip: You can install Tomcat to the system tray via the MS (Monitoring Service) option. This will allow you to start, stop, configure, etc. the service right from the system tray. Simply issue:

```
Tomcat7w //MS//
```

Troubleshooting: If Tomcat or your Windows service does not start, then you most likely entered the wrong memory settings. We have seen that assigning more then "1024m" to Tomcat does not start Tomcat at all. Note: This might be an issue on some 32bit Windows versions only.

___

**Permanent Memory Generation**

In some cases the server can run out of a different type of memory (Permanent Generation), and if this is the case the above settings may not help solve the memory issue. A problem like this may occur when running multiple applications on the same server.

If you are experiencing this type of error, you would most likely see the following error in your logs:

```
java.lang.OutOfMemoryError: PermGen space
```

To increase the level of this memory another java parameter will need to be added:

```
-XX:MaxPermSize=128m
```

**Linux**

As explained above all these settings take place in the setenv.sh. Add the following now;

```
export JAVA_OPTS="-Xms256m -Xmx512m -XX:MaxPermSize=128m"
```

**Windows (started manually)**

As explained above all these settings take place in the setenv.bat. Add the following now;

```
set JAVA_OPTS="-Xms256m -Xmx512m -XX:MaxPermSize=128m"
```

**Windows (started as a service)**

As mentioned above, for Windows services this is done by editing the service.