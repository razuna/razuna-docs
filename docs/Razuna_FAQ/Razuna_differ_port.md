**Running Razuna on a different port**

By default, Razuna Standalone runs on port **8080** (and hence is available at (http://<yourserver>:8080, eg. [http://localhost:8080](http://localhost:8080)).

If you want to run another Razuna instance but already has a service claiming port **8080**, there will be a conflict, and Razuna will fail to start. You may see errors like this:

```
LifecycleException: Protocol handler initialization failed: java.net.BindException: Address already in use:8080 
```

This can be fixed by changing Razuna to use another listening port (eg. **8090**) and shutdown port (eg. **8015**). This is done by editing conf\server.xml.

In order to change the port you have to edit the file "server.xml" in the folder "/razuna/tomcat/conf/". Change the line:

```
<Server port="8005" shutdown="SHUTDOWN">
```

to

```
<Server port="8015" shutdown="SHUTDOWN">
```

and the line:

```
<Connector port="8080" protocol="HTTP/1.1" ...
```

to

```
<Connector port="8090" protocol="HTTP/1.1" ...
```

Save the file to apply your changes.

Then restart Razuna and point a browser to http://<yourserver>:8090 (eg. [http://localhost:8090](http://localhost:8090)). 

> If you are running on a Unix server and bind the ports below 1024 (such as port 80 for example), you will need to start Razuna as root in order to successfully bind to the port


**Which port number should I choose? **

If you are not sure which port number to choose, use a tool such as netstat to determine which port numbers are free to use by Razuna. The highest port number that can be used is 65535 because it is the highest number which can be represented by an unsigned 16 bit binary number. The [Internet Assigned Numbers Authority (IANA)](http://www.iana.org/assignments/port-numbers) lists the registration of commonly used port numbers for well-known Internet services, it's advisable to avoid any of those ports. 

**A note about firewalls**

When you choose a port number for Razuna, bear in mind that your firewall may prevent people from connecting to Razuna based on the port number. Organisations with a local network protected by a firewall typically need to consider modifying their firewall configuration whenever they install a web-based application (such as Razuna) that is running on a new port or host. Even personal laptop and desktop machines often come with firewall software installed that necessitates the same sort of change as described above.

If Razuna does not need to be accessed from outside the firewall, then no firewall configuration changes will be necessary. 

