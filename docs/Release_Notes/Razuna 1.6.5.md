**Release Notes for Razuna 1.6.5**

**Notes for this release**

1.6.5 release features many exciting new features and enhancements. The most important change has been the possibility to use the **API as a user**!

In previous versions, the API was just available for an Administrator. Which meant that you had to build an application that provided everything to the user. In short, you had to take care of the permissions on the endpoint. This of course, was out of sync with the permissions of the user within Razuna. Needless to say that this was not the most optimal solution.

As of Razuna 1.6.5 you can **now build an application and give your users access with their own API Key**. Users will only see what they are allowed to see (according to their group level and permission) in your application. In other words, you do not need to worry about access to folders and files anymore on your end, as the API takes care of this now.

Razuna 1.6.5 comes with over 200 issues tackled. Many issues are fulfilled feature requests or enhancements to existing functionality.

___

**How to upgrade**

You should update to 1.5.2 before updating to 1.6! If you have already done so, then simply follow the [Razuna Update Guide](/installation/Upgrade/).

If you are skipping certain version then please make sure to read up on the release notes on each version. There might be instructions for certain updates!

___

**New Features**

* **API available to all users:** Using the API is now available to all users and not just administrators and the API requests will return the assets available to the user based on their permissions. Look for your API key under user info.

* **Folder Subscribe:** You can now subscribe to folders to be notified of any changes made to the assets that it contains. [View Snapshot](/Release_Notes/img/folder_subscribe.jpg)

* **User Expiry Date:** You can now choose to enter an expiry date for users after which time the user will not be able to login to the system. [View Snapshot](/Release_Notes/img/User_Expiry_Date.jpg) 

* **Asset Expiry Date:** You can now specify expiry date for assets after which time the asset will no longer be available to any users with 'Read Only' permissions on asset. On expiry the asset is labelled with an 'Asset has expired' label and the download links are expired. The ability to create new renditions or versions and modify its sharing options is also no longer available. [View Snapshot](/Release_Notes/img/custom_fields.jpg)

* **Show custom fields in 'Information' tab:** You can now choose custom fields to be displayed in the information tab of the asset details window. [View Snapshot](/Release_Notes/img/custom_fields.jpg)

* **Customize User Welcome Email:** You can now customize the welcome email for new users. [View Snapshot](/Release_Notes/img/new_user_welcome.jpg)

* **Download folder structure mimics Razuna structure:** Bulk downloads of assets from Razuna (e.g. Basket downloads) will now create the same folder structure as in Razuna.

* **Customize Export Template:** You can now choose what fields you want to export in the metadata export. Turning on this feature will also automatically include a metadata export file in all bulk asset downloads. [View Snapshot](/Release_Notes/img/export_template.jpg)

* **Copy Folder:** Folders can now be copied to other folders. Available only for local storage.

* **Universal Product Code Enabled:** Razuna now supports UPC for images. To read more about how to use this feature please see UPC Notes.

* **Upload additional versions and renditions:** You can now bulk upload additional renditions and additional versions

* **Replacing and archiving existing assets:** You can replace existing assets in bulk via uploading of a "RazunaVersions.zip" compressed file containing the new assets. The existing assets will be archived and can be found under the "Versions" tab.

      * **Rules :**

           * The compressed archive must have 'RazunaVersions' in its name.

           * User must be an administrator.

           * With the above 2 rules fulfilled the system will check to see if a file with the same name already exists for the host and if so it will archive it and replace it with the new one.

           * There must be only instance of the file with the filename, if multiple found then file will be added as a new file.

           * If file not found to be existing then it will be treated as a new file and added as usual.

           * Files in trash are ignored when checking for existence of file.

* **Versions available to all users:** Ability to upload versions of assets is now available to all users whereas it was only previously available to administrators.

* **Copy metadata to renditions option:** If you want the metadata from original file to be copied to renditions on save then simply turn on this option. [View Snapshot](/Release_Notes/img/rendition_meta_copy.jpg)

* **Download filename without extension option:** If you want Razuna to download the file with the filename as is and not add a file extension to it then turn on this option. Only applicable to individual file download links and not bulk asset downloads.

* **Rendition size in pixels or inches:** You can now specify size of rendition to be created in inches. [View Snapshot](/Release_Notes/img/pix_or_in.jpg)

* **Thumbnail size calculations refinement:** Calculation of thumbnails is now much smarter. In settings you can now choose to set only either the height or width and the system will automatically calculate the remaining height/width while maintaining the aspect ratio. If both attributes are specified then the system will try and get the thumbnail to match the specified dimension as closely as possible while still maintaining the aspect ratio. [View Snapshot](/Release_Notes/img/thumb_settings.jpg)

* **Mail SSL and TLS options added:** Mail settings in administrator now have the ability to specify the SSL and TLS settings. This is needed if you wish to use a provider such as Gmail to work with Razuna. [View Snapshot](/Release_Notes/img/mail_settings.jpg)

* **Show recent updates:** In white labelling you can now choose to show recent updates of assets on the entry page displayed when user logs in. [View Snapshot](/Release_Notes/img/recent_updates.jpg)

* **Store metadata for additional renditions:** It is now possible to save metadata for additional renditions.

* **Metaform plugin 'Copy to all':** You can now choose to copy the value of a field for an asset on the metaform plugin to all other assets using the 'Copy to all' feature.

___

**All resolved issues of Razuna 1.6.5**

|Summary|Type|
|-------|----|
|[Option to copy values to other fields/records](http://issues.razuna.com/browse/RAZ-3073?src=confmacro)|Technical Task|
|[Set the radio button to false](http://issues.razuna.com/browse/RAZ-3072?src=confmacro)|Technical Task|
|[Outline which field is required (star next to it)](http://issues.razuna.com/browse/RAZ-3071?src=confmacro)|Technical Task|
|[Metaform plugin problem with custom fields for only one asset type](http://issues.razuna.com/browse/RAZ-3057?src=confmacro)|Technical Task|
|[Option to be able to set unit for resizing](http://issues.razuna.com/browse/RAZ-2924?src=confmacro)|Technical Task|
|[Apply custom field selection to file detail view (all types) ](http://issues.razuna.com/browse/RAZ-2836?src=confmacro)|Technical Task|
|[Add custom field selection to customisation for file detail window](http://issues.razuna.com/browse/RAZ-2835?src=confmacro)|Technical Task|
|[Add an expiration date to a user and disable access when expiration occurs](http://issues.razuna.com/browse/RAZ-2830?src=confmacro)|Technical Task|
|[Make outgoing email text customisable in .properties file ](http://issues.razuna.com/browse/RAZ-2818?src=confmacro)|Technical Task|
|[Option to set the email interval on update ](http://issues.razuna.com/browse/RAZ-2817?src=confmacro)|Technical Task|
|[Option to subscribe to folders ](http://issues.razuna.com/browse/RAZ-2816?src=confmacro)|Technical Task|
|[Final Testing Phase ](http://issues.razuna.com/browse/RAZ-3113?src=confmacro)|Task|
|[Update translation files ](http://issues.razuna.com/browse/RAZ-3111?src=confmacro)|Task|
|[Phase 3 testing ](http://issues.razuna.com/browse/RAZ-3110?src=confmacro)|Task|
|[Phase 2 Testing ](http://issues.razuna.com/browse/RAZ-3068?src=confmacro)|Task|
|[Add ability to output debugging info for client in Razuna ](http://issues.razuna.com/browse/RAZ-2933?src=confmacro)|Task|
|[Task 	Fix for merge issues ](http://issues.razuna.com/browse/RAZ-2876?src=confmacro)|Task|
|[Add "UPC enabled" option in Host Administration (under settings) ](http://issues.razuna.com/browse/RAZ-2852?src=confmacro)|Task|
|[Export templates ](http://issues.razuna.com/browse/RAZ-2831?src=confmacro)|Task|
|[As a user I want to see a thumbnail preview of my image renditions in Razuna ](http://issues.razuna.com/browse/RAZ-2839?src=confmacro)|Story|

Showing 20 out of [251 issues](http://issues.razuna.com/secure/IssueNavigator.jspa?reset=true&jqlQuery=fixVersion+%3D+%221.6.5%22+AND+project+%3D+RAZ+ORDER+BY+issuetype+DESC%2C+key+DESC+&src=confmacro)







