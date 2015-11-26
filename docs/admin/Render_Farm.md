**Razuna Rendering Farm**

> This feature is available as of Razuna 1.4.8

By default Razuna, transcodes all your assets on the local server. If you enable the rendering farm feature, you will be able to transcode your videos, images and audio assets on an external server farm. This will free up the ressources on this server and is the recommended way for large encoding transactions. It doesn't matter if your rendering server(s) are within your local network or instances on the cloud (Amazon EC2, VMWare, etc.).

___

**Install one rendering server first**

In order to setup one or many rendering server you need to install and run at least one rendering server before enabling it. Please refer to [Installing a Razuna Rendering Server](/installation/Render_Server/) to do so.

Once you have installed a Razuna Rendering Server, you can enable it here.

___

**Global Rendering Farm Settings**

![](/admin/img/rfs-features.jpg)

**Enable/Disable**
When you have setup at least one rendering server and verified that Razuna can reach the server, then enable the rendering farm with this switch. Caution: This option is applied immediately!

**Location**
This defines the location of this Razuna server. The location can be used for grouping rendering servers. The internal code will then look for servers within the same location and use those rendering servers. This parameter is optional and only needed if you have many Razuna servers and rendering servers at different locations. If you don't need this, then just leave the field empty.

___

**Add or edit a rendering server**

Each rendering server comes with its own settings as each rendering server will exchange data with this Razuna installation. You can add as many rendering servers as you need.

![](/admin/img/rfs-1.jpg)

**Activate**
Enable or disable this rendering server.

**Rendering server Address**
Enter the DNS name or the ip address of your rendering server. By default port 80 is used, if your rendering server runs on another port, say 8080, you will need to provide the port along with the address as in "rendering.local:8080". Click on validate to test the connection to the rendering server.

**Location**
Enter the name of your location here. This value should be in line with the default location value of this server. Like this we can group the rendering farm servers to one location. If you don't need this, then simply leave this field empty.

Click on the "Tools" tab to enter the paths to your libraries.

![](/admin/img/rfs-2.jpg)

As mentioned in the "[Installing a Razuna Rendering Server](/installation/Render_Sever/)" guide, you need to install the additional libraries. Enter here the absolute paths to these libraries. Please double check the paths to the libraries!

Click on save to add the rendering server. You can now enable the rendering farm option in order for Razuna to use your rendering farm server(s) for any new transcoding process.