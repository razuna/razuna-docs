**Upgrade from 1.1.4 to 1.2**

**Overview**

Razuna 1.2 is a big upgrade, both in the sense of feature set and enhancements. The list below is only a short list of new features we added for 1.2. You can always lookup the release notes and upcoming features of Razuna at the public Issue Tracker at [http://issues.razuna.com](http://issues.razuna.com).

**Version Control**

For each asset you now have a Version Control system. Thus whenever you upload a new version of your image, video or document, the original version will be saved and stored for you. Within the version tab you can then also play the version back, where as a new version of the current version is stored again.

**Initial Folder View and Folder Tree Navigation**

Many have asked for it, so we are very happy to give it to you. We now have a Folder-Navigation tree structure for you. No need to reload the folder navigation anymore. Also, we changed the initial folder view to show you all the assets, independently of the asset type, when you navigate to a folder.

**Commenting and sharing of a folder/collection**

Another demand that many have expressed is to be able to have a commenting section for each asset. This is now available with Razuna 1.2. You can comment on each asset within the "comments" tab. Furthermore, the commenting takes on a larges scale approach when you combine it with sharing. Sharing is a new feature, which allows you to share your folder or collection with the same users/groups within Razuna or simply with "Everyone". If you share a folder/collection with "Everyone", it will be available under a public URL for everyone to see. Moreover, each asset can be commented on. This is a great feature for all of you who need to share your work with clients or alike.

**Print to PDF**

Any asset, search result and folder view can now be converted to a PDF for printing. We setup a printing wizard which lets you choose the size of the paper, how many assets you want on a page, size, and more.

**Miscellaneous**

As mentioned there are many more enhancements. Like French translation, a Developer API, PSD, AI and EPS files are treated as images, we generate thumbnails and preview files for PDF files, Oracle support has been converted to support file system asset storage and we have a Razuna Desktop application ready to make uploading easy for everyone.

___

**Update Procedure**

You should always make a backup or Razuna and especially of your database before attempting any update! That said, this process of updating Razuna is quite simple.

 * Download and unarchive the latest release.
 * Stop the Razuna (or J2EE) server.
 * Copy the folders "admin" and "global" of the new version and drop them into your existing Razuna installation folder.
 * Start the Razuna (or J2EE) server.

___

**Update the Database**

After you have installed Razuna 1.2 you should navigate to [http://yourdomain/admin/update.cfm](http://yourdomain/admin/update.cfm). This will check if there is an update needed for your database. If so, then please run the update before continuing working with version 1.2.

___

**Update your hosts**

Log in to the Razuna Administration and navigate to "Settings/List/add Hosts" then apply the update to each host that you have in your list.

Your copy of Razuna is now updated and so are all hosts you have.


