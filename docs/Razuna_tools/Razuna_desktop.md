**Razuna Desktop**

> **Razuna Desktop no longer supported** : Due to continued issues with the AIR platform and inconsistency we have decided to stop the development of Razuna Desktop and concentrate on a different solution for the future.


Razuna Desktop is a Desktop application which allows you and your team to easily upload any asset right from your desktop to Razuna.

Razuna Desktop works both with the Razuna Hosted Platform and your own hosted Razuna deployment. It works on MacOS X, Windows and Linux.

If you haven't downloaded Razuna Desktop you can go over to our download page and get it there. Download Razuna Desktop

The current implementation of Razuna Desktop will upload all assets to the "Upload Bin" Folder of your Razuna account! This will change in a future version where we will allow to chose folders to upload to.

![](/Razuna_tools/img/razuna-desktop-small.png)

___

**Connect to Razuna**

**Razuna Hosted Platform (Hosted)**

To connect to your Hosted account you need to provide your subdomain, login name and password.

The subdomain is the one that you have chosen during the signup. As a example; if you registered "demo", then your subdomain would be "demo.razuna.com" (without the "http://" part).

If you want that you automatically login the next time when you start Razuna Desktop you should mark the "Remember" checkbox.

(Click on the thumbnail to see a bigger image)

![](/Razuna_tools/img/razuna-desktop-hosted.png)

**Razuna Self Hosted (Local)**

In order to connect to your own Razuna server you need to provide the host name of your server, user name, password, hostid and the path to your DAM.

**Host name**

The host name is the host to your server. If you access your local installation with a URL like "razuna.local:8080/demo/dam" then your host name is "razuna.local:8080".

> If your path is "razuna.local:8080/razuna/demo/dam" the you might have to use "razuna.local:8080/razuna" as your hostname!

![](/Razuna_tools/img/razuna-desktop-self.png)

**Host ID**

The Host ID can be found in the "Host Setup" of the Razuna Administration and is for each Host unique. You need to provide the correct Host ID for the host you want to connect to.

**DAM Path**

This is the second path of the URL you usually access with your browser. Meaning, if you access your installation in your browser with "razuna.local:8080/demo/dam" then your DAM path is "/demo/dam".

If you want that you automatically login the next time when you start Razuna Desktop you should mark the "Remember" checkbox.

(Click on the thumbnail to see a bigger image)

___

**Troubleshooting**

If you get an error saying "Login failed" then make sure that your subdomain, login name and password is correct.

Also make sure that connection to your Razuna account is not blocked by any firewall or filters. As a rule, if you can connect with your browser you should be able to connect with Razuna Desktop.


