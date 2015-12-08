**Batch Upload**

**Batch upload or adding many assets and folder structure at once**

Many times you want to add many assets or even a complete folder structure at once. Let's say you want to replace your existing file server with Razuna and need to preserve the folder structure and all assets within.

This task can be accomplished quite easily with Razuna. All you have to do is to create a ZIP archive of your folder structure and upload it to your Razuna server. Razuna will then extract the archive and add each asset and for each folder it will create a new folder and adding assets within as well.

> **Note** : For Razuna to know that a folder should be added it needs to have a file in each folder! That means if you have an empty folder in your archive it won't be added unless you will add a file to it (can and should be a text file which is empty).

___

**Example**

Let's say we have the following folder structure:

My Assets

-> subfolder 1

--> Movie.mov

--> asset.pdf

-> subfolder 2

--> mypic.png

-> subfolder 3

--> dummy.txt

In the folder structure above your folder structure within Razuna will be that all folders (subfolder 1,2,3) will be created within Razuna and assets in subfolder 1 + 2 will be added. Subfolder 3 will be created but since there is only a dummy.txt file with zero size only and empty folder is being created.

___

**How can I add the ZIP archive?**

It does not matter how you add the archive to Razuna. You can use the single upload, the server, eMail or FTP upload functionality.

___

**Tips**

You can automate uploading and adding of assets within Razuna. Have you or your administrator setup a "scheduled upload". With scheduled uploads you can automate adding of assets and create "watch folders". You can read more about ["Scheduled Upload" here](http://wiki.razuna.com/display/ecp/Scheduled+Uploads).