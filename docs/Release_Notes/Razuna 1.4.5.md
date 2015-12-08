**Release Notes for Razuna 1.4.5**

**Important Notes for this release**

Razuna 1.4.5 brings major enhancements and many important bug fixes to the 1.4.4 release.

**Widgets : Share or embed your folders / collections with ease**

Widgets can be setup for every folder or collection, you can even create as many widgets as you want for a given folder/collection, since each widget has different settings. Foremost, you can arrange your assets to be shown in the thumbnail grid or as a slideshow. Also, you will have a preview function for each asset and can download each one individually.

There are many good uses for widgets, as a example you can include a widget into your website, blog, create a photo archive and so forth.

**Browse Subfolders**

Coming in line with the release of Widgets, we also enabled browsing trough subfolders in the general folder view, the shared folders and of course within a Widget. Like this, especially in a shared folder/collection or widget, you can share any folder and your users will be able to drill down into all available subfolders.

**Add additional versions of an asset**

As more and more organizations start to move to Razuna, the need for a "unified view" of an asset was raised. Say, you have different versions of your assets already deployed, on YouTube, Vimeo, Flickr, and Soundcloud or simply want to upload each version of your already converted formats to Razuna. Previously, each upload created a new "asset record".

With the new "Additional Versions" functionality you can simply point to your existing asset on the net or upload your versions. Doing so, will give you a combined view, of your original asset, any converted formats and and your own versions.

**Small Re-Design, Lighter Interface**

We have done some small re-design of the Razuna User Interface. The goal was to get rid of the many shades and table lines, in short to bring a "lighter user experience" to the Razuna feeling.

**Overall changes**

Above we mentioned the most exciting features. Additionally, we have added full XMP support for PDF files (now we write to **ALL** XMP fields), for Administrators we added searching trough log files, fixed some bugs when Razuna was hooked up to a Amazon S3 account and fixed the uploading tool for the Google Chrome browser.

Overall, there are around 25 request issues that we are fulfilling with Razuna 1.4.5.

Last but not least, Developers have a reason to celebrate. With Razuna 1.4.5 we are introducing new options to the API. These are;

   * You are able to add metadata during uploading
   * You can retrieve informations about an asset with one call
   * Adding a user returns the generated userid

___
**How to upgrade**

You should update to 1.4.2 before updating to 1.4.5! If you have already done so, then simply follow the [Razuna Update Guide](/installation/upgrade/).

> **Upgrading from Razuna 1.4.4** : Due to a bug in the backup of 1.4.4 you might run into a issue when you try to backup your installation. Simply apply the hotfix available at [http://issues.razuna.com/browse/RAZ-809](http://issues.razuna.com/browse/RAZ-809) before upgrading to Razuna 1.4.5

___

**[All resolved issues of Razuna 1.4.5](http://issues.razuna.com/secure/IssueNavigator.jspa?reset=true&jqlQuery=fixVersion%20=%20%221.4.5%22%20AND%20project%20=%20RAZ%20ORDER%20BY%20issuetype%20DESC,%20key%20DESC&tempMax=1000&src=confmacro) (28 issues)**

|Summary|Type|
|-------|----|
|[API: Add metadata during upload ](http://issues.razuna.com/browse/RAZ-830?src=confmacro)| Improvement    |
|[Enable all metadata read and write for PDF ](http://issues.razuna.com/browse/RAZ-821?src=confmacro)| Improvement    |
|[Widgets: Allows for embedding folders/collections in any site ](http://issues.razuna.com/browse/RAZ-820?src=confmacro)| Improvement    |
|[Additional Versions: Link to existing content (URL) and option to upload additional versions ](http://issues.razuna.com/browse/RAZ-806?src=confmacro)|Improvement     |
|[Option to search the logs ](http://issues.razuna.com/browse/RAZ-803?src=confmacro)|Improvement     |
|[API: Get single asset information ](http://issues.razuna.com/browse/RAZ-798?src=confmacro)|Improvement     |
|[Show subfolders in folder view, in the shared view and in widgets ](http://issues.razuna.com/browse/RAZ-552?src=confmacro)|Improvement     |
|[API: Adding a user returns the user id ](http://issues.razuna.com/browse/RAZ-828?src=confmacro)| Improvement    |
|[Share: Small Re-Design ](http://issues.razuna.com/browse/RAZ-816?src=confmacro)| Improvement    |
|[Small re-design for the table views and listing (make it lighter, less is more) ](http://issues.razuna.com/browse/RAZ-815?src=confmacro)| Improvement    |
|[Windows: Fails if more then 3 formats are selected for converting a image ](http://issues.razuna.com/browse/RAZ-832?src=confmacro)| Bug   |
|[Login credentials persist after logout ](http://issues.razuna.com/browse/RAZ-831?src=confmacro)|  Bug  |
|[Search did not allow all illegal chars as the first char. Should only be * and ? ](http://issues.razuna.com/browse/RAZ-829?src=confmacro)| Bug   |
|[Upload Templates: Bitrates were not reflected in the frontend ](http://issues.razuna.com/browse/RAZ-827?src=confmacro)|Bug    |
|[API: Fix path to asset ](http://issues.razuna.com/browse/RAZ-823?src=confmacro)|Bug    |
|[Basket: Did not reflect converted formats ](http://issues.razuna.com/browse/RAZ-819?src=confmacro)|Bug    |
|[Share: Basket download did not work under some circumstances ](http://issues.razuna.com/browse/RAZ-818?src=confmacro)|Bug    |
|[Share: Assets were not properly put into the basket in the list view ](http://issues.razuna.com/browse/RAZ-817?src=confmacro)|Bug    |
|[Showing details of an audio asset could take a very long time, thus Razuna running out of memory ](http://issues.razuna.com/browse/RAZ-814?src=confmacro)| Bug   |
|[Version: Not properly working especially together with Amazon S3, Eucalyptus and Nirvanix ](http://issues.razuna.com/browse/RAZ-813?src=confmacro)|Bug    |

Showing 20 out of [28 issues](http://issues.razuna.com/secure/IssueNavigator.jspa?reset=true&jqlQuery=fixVersion%20=%20%221.4.5%22%20AND%20project%20=%20RAZ%20ORDER%20BY%20issuetype%20DESC,%20key%20DESC&tempMax=1000&src=confmacro) 
