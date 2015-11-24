**Release Notes for Razuna 1.7**

**Notes for this release**

Razuna 1.7 features many useful features and enhancements that will make your work with files easier. Please have a look at the overview below to see what is new or changed.

Razuna 1.7 comes with over 150 issues tackled. Many issues are fulfilled feature requests or enhancements to existing functionality.

___

**How to upgrade**

You should update to 1.5.2 before updating to 1.6! If you have already done so, then simply follow the [Razuna Update Guide](/installation/Upgrade/).

If you are skipping certain version then please make sure to read up on the release notes on each version. There might be instructions for certain updates!

___

**New Features**

* **Aliases:** You can create aliases within folders now. Select a file, create an alias for that file in another folder and you got a link between these files. Aliases behave just like their original file.

* **Import of custom XMP metadata:** Import custom metadata from any other system with ease in Razuna 1.7. Create a custom field in Razuna and define the XMP-Path of the metadata. Razuna will automatically parse the XMP metadata and enter the value into the custom field.

* **Customize Search:** You can lock down the search to folders only. To enable go to Administration>Customization>Search>Enable folder search selection.

Once enabled you will see a new checkbox under folder settings (Folder Sharing & Settings link in folder view) titled 'Search selection'.

![](/Release_Notes/img/searchenable.jpg)

* **Search and Label View:** We are happy to announce that a long standing request by the Razuna community has been satisfied with 1.7. In short, the label and the search view have now (almost) all the functionality you can find in the standard folder view.

* **White-Labelling:** White-Labelling is now available per host! Look under Host Administration>White-Labelling.

* **Customization:** Razuna 1.7 has now even more customization options.

     * Each icon, button, tab, etc. can now be made accessible to certain groups only (instead of show/hide for everyone). 

     * Option to redirect users to folders can now be assigned per group.

     * Metadata can now be shown on top of the file and at the bottom (previously only at the bottom).

     * Labels for each metadata field can now be turned off.

* **Administration:** The administration can now be made accessible to certain members of a group. Previously, you had to be an Administrator of the host to be able to access the Administration.

* **Thumbnails:** You can now upload a thumbnail for document type files (thus replacing the default Word, ZIP, etc. icon).

* **Folder Tree:** Finally long folder names do not simply extend but wrap properly (Yeah!)

* **Expanded LDAP/AD support:** The LDAP/AD setup under Administration has been expanded to allow for more seamless integration with Razuna. [See LDAP/AD Setup](/admin/LDAP Services/).

* **Folder counts:** A summary of asset counts in folders is now available under Administration>Logs>Folder Summary.

* **Inherit share permissions to sub-folders:** Sharing permissions can now be automatically inherited to sub-folders. [See snapshot](/Release_Notes/img/share_inherit.jpg).

* **Renditions:** It is now possible to swap the original file with an additional rendition for document type assets.

___

**All resolved issues of Razuna 1.7**

|Summary|Type|
|-------|----|
|[Disable search all in search selection](http://issues.razuna.com/browse/RAZ-3259?src=confmacro) |Technical task|
|[Re-factor folder search](http://issues.razuna.com/browse/RAZ-3252?src=confmacro) |Technical task|
|[Add folder selection to advanced search](http://issues.razuna.com/browse/RAZ-3244?src=confmacro) |Technical task|
|[Replace quick search drop down with folder selection](http://issues.razuna.com/browse/RAZ-3243?src=confmacro) |Technical task|
|[Change it so News and Frontpage can be customized per Host](http://issues.razuna.com/browse/RAZ-3203?src=confmacro) |Technical task|
|[Option to completely remove the front page and replace it with custom HTML](http://issues.razuna.com/browse/RAZ-3202?src=confmacro) |Technical task|
|[Customise Notification](http://issues.razuna.com/browse/RAZ-3165?src=confmacro)|Technical task| 
|[On asset expiration send out notification to groups](http://issues.razuna.com/browse/RAZ-3163?src=confmacro)|Technical task|
|[Add group to notification automatically](http://issues.razuna.com/browse/RAZ-3162?src=confmacro)|Technical task|
|[1.7 Final Changes](http://issues.razuna.com/browse/RAZ-3369?src=confmacro) |Task|
|[Investigate 'Failed to extract zip file. Check the file is a valid zip file.' errors](http://issues.razuna.com/browse/RAZ-3362?src=confmacro)| Task|
|[1.7 Testing](http://issues.razuna.com/browse/RAZ-3348?src=confmacro) |Task|
|[Remove add asset via email feature](http://issues.razuna.com/browse/RAZ-3316?src=confmacro) |Task|
|[API: Option to sign in with an API key and user email address](http://issues.razuna.com/browse/RAZ-3354?src=confmacro) |New Feature|
|[Show complete folder breadcrumb in search results](http://issues.razuna.com/browse/RAZ-3349?src=confmacro)|New Feature| 
|[Hosted editions should be able to import from server path too](http://issues.razuna.com/browse/RAZ-3328?src=confmacro) |New Feature|
|[Make "redirect to folder" a per group option](http://issues.razuna.com/browse/RAZ-3311?src=confmacro) |New Feature|
|[Import of custom namespaces in XMP to custom fields](http://issues.razuna.com/browse/RAZ-3292?src=confmacro)|New Feature| 
|[Option to swap original with a rendition](http://issues.razuna.com/browse/RAZ-3279?src=confmacro)|New Feature| 
|[Change "choose thumbnail" to be able to choose from rendition thumbnails](http://issues.razuna.com/browse/RAZ-3278?src=confmacro) |New Feature|

Showing 20 out of [199 issues](http://issues.razuna.com/secure/IssueNavigator.jspa?reset=true&jqlQuery=fixVersion+%3D+%221.7%22+AND+project+%3D+RAZ+ORDER+BY+issuetype+DESC%2C+key+DESC+++++&src=confmacro)