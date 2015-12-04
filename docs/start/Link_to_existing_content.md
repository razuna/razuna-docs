**Link to existing content**

With this functionality you will be able to link to existing content on your network volumes or content that exists outside of your network (Internet websites, Flickr, YouTube, etc.)

When you "link to content" the assets themselves will **not** be moved to the internal structure of Razuna, but will stay at their original location. The benefit of this method is that you don't have to upload assets to Razuna (thus processing is much faster) and you can use Razuna as a web frontend to your existing file server infrastructure. Moreover, you can still access your asset on the fileserver plus Razuna gives you the option to convert the assets to others formats.

There are two way to link to existing content. One is the linking to single assets the other to a complete folder structure.

___

**Link to single assets**

You can link to existing assets within the "Add file(s)" dialog. Within the tab "Link to Content" you then have to option link to content on a public URL (URL's which are publicly accessible by your browser), enter the embed code of a video player (YouTube embed code, etc.) or enter the absolute path to an asset on your network (path has to be accessible by Razuna).

> *Linking to assets is not available on the Razuna Hosted Platform*

Enter the appropriate values into the chosen fields and click on "Add Asset" to add the asset to the folder.

![](/start/img/linktocontent.jpg)


___

**Link to Folders**

> *Linking to folders is not available on the Razuna Hosted Platform*

When you add a folder you additionally have the option to "Link to a Folder". With this function you can use Razuna to index a complete folder structure on your network.

To add a folder you simply need to enter the **absolute path** to your folder in the text input field. Say your folder name is "marketing" and the path would be "/opt/company/", then your absolute path would be "/opt/company/marketing". Click on the "Check Folder" link in order to test if Razuna can read the location given. If so, then you can simply create the link to the folder by clicking on "Add".

> By creating a link to a folder, Razuna will recreate the folder structure within the **internal Razuna structure** and will create a preview of each single asset within the given folder structure. Razuna **WILL NOT** temper with the original folder structure or assets of the given path! 

> If you have a lot of assets and sub-folders, this process can take a while!

![](/start/img/linktofolder.jpg)

___

**How to work with "linked" assets**

Working with a linked folder or asset is just like working with an asset that you have uploaded into Razuna. The only difference is that you will not be able to create a version of the asset. Furthermore, you will not be able to view the original asset within Razuna. After all Razuna is a web application and thus certain restrictions of file access are given for a web application. As such, Razuna can not "look" into your file structure or network. Would that be possible for web application many security problems would arise!

But apart from that, all functionalities are available. Especially useful is the option to convert the asset to different formats. This will then bring the assets "into" the internal Razuna structure and would allow access directly trough Razuna again.

In order for you to recognize linked assets we notify you within the editing window of a linked asset.

![](/start/img/linkedasset.jpg)

> If you decide to remove a linked folder or a linked asset, **ONLY** the information within Razuna will be removed. Razuna **WILL NOT** remove the original folder!