**Installing the Search Server**

> *You only need to follow the below instructions if you want to run the Razuna Search Server on its own Server or even on a dedicated hardware. Only perform the below steps AFTER you have upgrade to Razuna 1.7.5!*

The Razuna Search Server can greatly improve performance. The Razuna Search Server can be located within your local network, on a virtual machine, as a virtual server in the cloud (Amazon EC2, etc.) or wherever it fits you best. The Razuna Search Server works with all storage options (Local or Cloud Storage).
___

**Requirements**

In order to run the Razuna Rendering Server you need to install the following:

 * A J2EE server (Tomcat recommended)
 * Java installed (Java 7)
 * A centralized database for your Razuna installation (Razuna and the Razuna Search Server(s) need to be able to connect to it)
 * If your storage option is "local" the Search Server needs to have access to the files (NFS recommended)

___

**Get the Razuna Search Server application**

The Razuna Rendering Server application is an additional application that needs to run on top of your J2EE server. You can download the latest edition from [https://github.com/razuna/razuna-searchserver](https://github.com/razuna/razuna-searchserver). Once downloaded copy the application into the "webapps" folder of Tomcat..

Start or restart the Tomcat server. You can test if the application is running successfully by going to the application directly in your browser with [http://dnsname:8080/razuna-searchserver](http://dnsname:8080/) (or IP address).

___

**Configure Razuna to use the dedicated Search Server**

In order to change from the local search server to the dedicated one you need to configure this in the main Razuna server. Go to the backend Administration and then to "General Configuration" and click on the tab "Indexing".

![](/installation/img/Digital_Asset_Management.png)

Make sure to select **"Dedicated Server"** and enter the complete URL to the search-server. In our example this is "http://localhost:8090/razuna-searchserver". Click "SAVE" to update Razuna.

Once done, we need to tell the Search Server to use the same database as Razuna. Click on the **"Search Server Database Connection"** link. In the following window enter the connection to your database. This should be the **same settings** as Razuna uses!

![](/installation/img/Digital_Asset_Management.png)

After you've entered all required information, click on the button. This will establish a connection to your Search Server and setup the database connection. If it can do so successfully it will let you know in a message. After that you can close this window.

