**Tenant Customization**

> **Available as of Razuna 1.5** : This option was introduced in Razuna 1.5.

___

**Customizing Razuna**

Customizing is something that you might want to do in order to embed Razuna into your application or simply are in need to disable certain functions. Since Razuna is a open source application you can of course, change the code and achieve a certain type of customization in this regard, but you will loose an easy way to upgrade to new releases. Thus, we provide the option of customization.

___

**Design**

**show top part**

![](/admin/img/razuna-top.jpg)

**show bottom part**

![](/admin/img/razuna-bottom.jpg)

If you set both of the above parameters to "hide" you will be left with a design of only the middle main section of Razuna. This might come in handy if you simply want to include Razuna in another application via iFrame.

> **Admin & Search functions** : In case, that the upper part is hidden and there are Administration-Functions and a search field available, we show an Administration (only visible to Administrator) and a Search Panel on the main page, mirroring the same options.

In case, you would hide the upper and bottom part Razuna would then be displayed like this (sample screen shot taken from Razuna 1.5):

![](/admin/img/razuna-middle.jpg)

___

**Explorer**

|Parameter|Action|
|---------|------|
|tab collections|Show/hide the Collection tab in the left explorer menu. NOTE: This will also disable the option to create and use collections!|
|tab labels|Show/hide the Labels tab in the left explorer menu. NOTE: This will also disable labeling any assets, folders or collections!|

These settings apply to the explorer on the left side within Razuna as displayed below:

![](/admin/img/razuna-explorer.jpg)

___

**Upload**

|Parameter|Action|
|---------|------|
|tab add from server|Show/hide the "Add from Server" tab within the upload widget.|
|tab add from email|Show/hide the "Add from eMail" tab within the upload widget.|
|tab add from ftp|Show/hide the "Add from FTP" tab within the upload widget.|
|tab add from link|Show/hide the "Add from Link" tab within the upload widget.|

___

**Folderview**

|Parameter|Action|
|---------|------|
|tab images|Show/hide the "Images" tab in the folder views.|
|tab videos|Show/hide the "Videos" tab in the folder views.|
|tab audios|Show/hide the "Audios" tab in the folder views.|
|tab other|Show/hide the "Other Formats" tab in the folder views.|
|tab pdf|Show/hide the "PDF" tab in the folder views.|
|tab doc|Show/hide the "Doc" tab in the folder views.|
|tab xls|Show/hide the "Xls" tab in the folder views.|
|icon select|Show/hide the "Select" icon in the folder views.|
|icon refresh|Show/hide the "Refresh" icon in the folder views.|
|icon show subfolder	|Show/hide the "Show Subfolders" icon in the folder views.|
|icon create subfolder	|Show/hide the "Create Subfolders" icon in the folder views.|
|icon favorite folder|Show/hide the "Favorite Folder" icon in the folder views.|
|icon search|Show/hide the "Search within Folder" icon in the folder views.|
|icon print|Show/hide the "Print Assets" icon in the folder views.|
|icon rss|Show/hide the "RSS" icon in the folder views.|
|icon word|Show/hide the "Show in Word" icon in the folder views.|
|icon metadata import	|Show/hide the "Import Metadata" icon in the folder views.|
|icon metadata export|Show/hide the "Export Metdata" icon in the folder views.|
|icon download folder|Show/hide the "Download all assets in this Folder" icon in the folder views.|

The above "TAB_" parameters apply to all tabs in all folder views, e.g the above "ICON_" parameters apply to the list of icons within all folder views. NOTE: The Tabs: "Folder Properties", "Sharing", and "Widgets" are shown to groups within permissions only. The tab "Content of this folder" is always shown as it contains all assets in this folder and is the entry point of any folder for the users.

![](/admin/img/razuna-folder-view.jpg)

___

**Assetview**

|Parameter|Action|
|---------|------|
| tab description keywords    | Show/hide the "Description & Keywords" tab in the asset view window.    |
| tab custom fields    | Show/hide the "Additional Metadata" tab in the asset view window.    |
| tab convert files    |  Show/hide the "Create Rendition(s)" tab in the asset view window.   |
| tab comments    | Show/hide the "Comments" tab in the asset view window.    |
| tab metadata   |  Show/hide the "Metadata" tab in the asset view window.   |
| tab xmp description   | Show/hide the "XMP Description" tab in the asset view window.   |
| tab iptc contact    |  Show/hide the "IPTC Contact" tab in the asset view window.   |
| tab iptc contact   |  Show/hide the "IPTC Contact" tab in the asset view window.   |
| tab iptc image   | Show/hide the "IPTC Image" tab in the asset view window.    |
|tab iptc content     | Show/hide the "IPTC Content" tab in the asset view window.    |
|tab iptc status     |  Show/hide the "IPTC Status" tab in the asset view window.   |
|tab origin     | Show/hide the "Origin" tab in the asset view window.    |
|tab versions     |Show/hide the "Versions" tab in the asset view window.     |
|tab sharing options	     | Show/hide the "Sharing Options" tab in the asset view window.    |
|tab preview images     |Show/hide the "Preview Image" tab in the asset view window.     |
|tab additional renditions     | Show/hide the "Additional Renditions" tab in the asset view window.    |
|tab history     |Show/hide the "History" tab in the asset view window.     |
|button send email     |Show/hide the "Send by Email" button the asset view window.     |
|button send ftp     |Show/hide the "Send by FTP" button the asset view window.     |
|button basket     | Show/hide the "Put into Basket" button the asset view window.    |
|button add to collection    |  Show/hide the "Add to Collection" button the asset view window.   |
|button print    | Show/hide the "Print Details" button the asset view window.    |

The above "TABS_" parameter apply to all asset types as do the "BUTTON_"parameters as show below:

![](/admin/img/razuna-assetview.jpg)

___

**Apply customization to all tenants**

> **Razuna 1.5.5** : This option is available as of Razuna 1.5.5!

In order to apply the customization to all your tenants, you can simply mark the checkbox next to the Save button entitled "Apply to all tenants". This will then copy all your changes to all the tenants.

**NOTE:** *This option is only visible if you log in to the tenant with your SystemAdministrator account!*




