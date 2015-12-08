**Razuna with Apache 2.x as a front end server**

**Fronting Razuna with the Apache 2.x web server**

There are many advantages to fronting the default J2EE server (Tomcat 6.x) that comes with Razuna. One of them is to load the static files off to Apache, while Tomcat only serves the dynamic content.

There are 2 kind of adapter to talk to Tomcat. There is the "native" HTTP protocol and the other is the AJP one. We do recommend the HTTP one.

___

**Configure Tomcat and Apache for HTTP**

By default Tomcat comes with the native HTTP protocol enabled. So there is actually nothing to do on the Tomcat side.

> For Apache to pass off requests to Tomcat you need to enable the "mod_proxy" and "mod_proxy_http" modules. How to do this depends on your Linux distribution. On Ubuntu it is a simple command like "a2enmod proxy_http". If you want to use SSL only also add the "Headers" module.

Once done you can configure a virtual host to pass on requests to Tomcat. Below you will find a example configuration:

```
<VirtualHost *:80>
        ServerName localhost
        DocumentRoot (absolute path to your razuna directory)
        ErrorLog /var/log/apache2/error_razuna.log
        CustomLog /var/log/apache2/razuna.log combined
 
        # Possible values include: debug, info, notice, warn, error, crit,
        # alert, emerg.
        LogLevel warn
 
        ProxyRequests Off
        <Proxy *>
                Order deny,allow
                Allow from all
        </Proxy>
 
        RequestHeader append x_https "on"
 
        ProxyPreserveHost On
        ProxyTimeout 120
        ProxyVia On
        ProxyPass / http://localhost:8080/
        ProxyPassReverse / http://localhost:8080/
 
        RewriteEngine On
        RewriteRule ^/(.*\.cf[cm]/?.*)$ http://localhost:8080/$1 [P]
</VirtualHost>
```

With this virtual host container we actually tell Apache to request any static file from the razuna directory and any static content from Tomcat (this is done with the rewriteEngine rules at the bottom).

___

**Configure Tomcat and Apache for AJP**

By default Tomcat comes enabled with the AJP protocol. If not, make sure the following like is not commented:

```
<Connector port="8009" protocol="AJP/1.3" redirectPort="8443" connectionTimeout="200000"
useBodyEncodingForURI="true" enableLookups="false" />
```

If commented, restart Tomcat after you changed this line.

Now all there is to do is to tell Apache to get the dynamic pages from Tomcat.

> In order to have AJP working in Apache you will need to include the mod_proxy_ajp.mod in your apache configuration. On CentOS/RedHat simply uncomment the lines in the http.conf file, for Ubuntu do a "sudo a2enmod mod_proxy_ajp.conf"

```
<VirtualHost *:80>
        ServerName localhost
        DocumentRoot (absolute path to your razuna directory)
        ErrorLog /var/log/apache2/error_razuna.log
        CustomLog /var/log/apache2/razuna.log combined
 
        # Possible values include: debug, info, notice, warn, error, crit,
        # alert, emerg.
        LogLevel warn
 
        ProxyRequests Off
        <Proxy *>
                Order deny,allow
                Allow from all
        </Proxy>
 
        RequestHeader append x_https "on"
 
        ProxyPreserveHost On
        ProxyTimeout 120
        ProxyVia On
        ProxyPass / ajp://localhost:8009/ ping=5 timeout=120
        ProxyPassReverse / ajp://localhost:8009/
 
        RewriteEngine On
        RewriteRule ^/(.*\.cf[cm]/?.*)$ http://localhost:8009/$1 [P]
</VirtualHost>
```

With this virtual host container we actually tell Apache to request any static file from the razuna directory and any static content from Tomcat (this is done with the rewriteEngine rules at the bottom).

