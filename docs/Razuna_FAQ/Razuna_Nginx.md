**Razuna with Nginx as a front end server**

___

**Fronting Razuna with the Nginx web server**

[Nginx](http://wiki.nginx.org/) is a small but powerful web server. Nginx is known for its high performance, stability, rich feature set, simple configuration, and low resource consumption.

All our websites our powered with Nginx and we have nothing but good experiences with it. Especially the low resource consumption and stability and a big plus. In our tests, Nginx performs around 20% better then Apache, given Nginx and Tomcat are configured correctly. Please follow the guidelines below.

___
**Configure Tomcat**

Nginx can not use the AJP protocol, so it is of no use together with Nginx. But it is of utmost importance that APR is configured. Thus the first step is to configure APR for Tomcat.

___

**Enable APR (Tomcat Native Library)**

Tomcat can use the Apache Portable Runtime to provide superior scalability, performance, and better integration with native server technologies. APR has many uses, including access to advanced IO functionality (such as sendfile, epoll and OpenSSL), OS level functionality (random number generation, system status, etc), and native process handling (shared memory, NT pipes and Unix sockets).

> You can also follow the installation directives from the [official Tomcat Native Library page](http://tomcat.apache.org/native-doc/)

**Linux**

The following steps are for Ubuntu, but they are about the same on any other Linux distro.

* Make sure that you have the libssl-dev and libapr1-dev packages installed$ apt-get install libssl-dev libapr1-dev

* Switch to your tomcat's bin directory$ cd $(TOMCAT_HOME)/bin

* Extract the tarball (tarred and gzipped archive) of the tomcat native lib$ tar -xvzf tomcat-native.tar.gz

* Jump into the source folder$ cd tomcat-native-xxx/jni/native

* Configure, make and install it: ./configure --with-apr=/usr/bin/apr-1-config && make && sudo make install

* Change to the system library folder$ cd /usr/lib

* Make a convenience link to you new library$ sudo ln -s /usr/local/apr/lib/libtcnative-1.so libtcnative-1.so

* Edit $(TOMCAT_HOME)/bin/catalina.sh adding the following lines:
  
```
LD_LIBRARY_PATH=/usr/lib:$LD_LIBRARY_PATH

export LD_LIBRARY_PATH
```

* Restart Tomcat.

**Note**: Some systems need to have IPv6 disabled in order to have APR working. Check your catalina.out log to see if APR is working.

**MacOS X**

Make sure to have installed the latest version of MacPorts.

1. From the Terminal program, enter:sudo port install tomcat-native.

2. From the Terminal program, make symbolic links from the /opt/local/lib/libtcnative-1.* to /usr/lib/java:sudo ln -s /opt/local/lib/libtcnative-1.* /usr/lib/java

3. Restart Tomcat

**Windows**

1. Download the APR library directly from Tomcat Native Library page.

2. Copy tcnative-xx.dll to %TOMCAT_HOME%/bin

3. Restart Tomcat.

___
**Configure Nginx**

Now all there is to do is to tell Nginx to get the dynamic pages from Tomcat.

> The below configuration is meant for people who know what they are doing and have already installed Nginx.

Edit your "razuna" virtual host config file (create it) (Ubuntu: sites-available/razuna) and add the following lines:

```
server {
  listen          80 default;
  server_name     _;
  root            /opt/tomcat/webapps/razuna;
  location / {
    proxy_pass              http://localhost:8080;
    proxy_set_header        X-Real-IP $remote_addr;
    proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header        Host $http_host;
    proxy_max_temp_file_size 0;
    expires     off;
    proxy_buffering off;
    proxy_store         off;
    proxy_connect_timeout 120;
    proxy_send_timeout    120;
    proxy_read_timeout    120;
 
  # All POST requests go directly
  if ($request_method = POST) {
    proxy_pass http://localhost:8080;
    break;
  }
}
 
  location ~ \.cfm$ {
    proxy_pass              http://localhost:8080;
    proxy_set_header        X-Real-IP $remote_addr;
    proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header        Host $http_host;
    proxy_max_temp_file_size 0;
    #proxy_redirect     off;
    expires             off;
    proxy_buffering off;
    proxy_store         off;
    proxy_connect_timeout 120;
    proxy_send_timeout    120;
    proxy_read_timeout    120;
  # All POST requests go directly
  if ($request_method = POST) {
    proxy_pass http://localhost:8080;
    break;
  }
}
 
}
```

Of course, adjust the path settings and individual settings to your environment. But with this we actually tell Nginx to request any static file from the Razuna directory and any static content from Tomcat.