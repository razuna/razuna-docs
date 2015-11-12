Welcome to Razuna System. In this page , we will show you how to use our system to manage the data in smoothly.

### Login :

Firstly user can login to system by account (username and password) which provided by System Admin or by Social accounts.

![Quick start](img/razuna_login.jpg)

In the next stage , from the first screen of the Razuna system. We can see the structure of the folders from the left side within folder names. Besides of this , user able to browse the files follow the Collection , Smart folders or Labels. 

To browse the file follow the Collection or Smart folder or Labels. Please click into "Folders" on top of the folder structure and choose one kind of search for browsing.

![](img/first_screen.jpg)

![](img/folder_structure.jpg)
___
### Quick Search :

The search engine of Razuna is based on the [Lucene](http://lucene.apache.org/) search engine. Lucene is a open source search engine and is part of the Apache Group. Lucene features among others useful functionalities phrase queries, wildcard queries, proximity queries, range queries and more.

**How to Search an asset :**

The "quick search" of Razuna searches within the following fields; **filename, keywords, description, file contents (e.g. all words in a PDF or word document), ID, labels and custom fields (user created)**. If you want to search in other fields, then use the advanced search or create your own field search that you can use in quick search.
___
**Case - Sensitive :**
The search is not case sensitive.
___
**Terms :**

There are two types of terms: Single Terms and Phrases.

A Single Term is a single word such as test or hello.

A Phrase is a group of words surrounded by double quotes such as "hello dolly".

Searching for hello dolly without quotes will search for terms matching hello AND terms matching dolly in the index i.e. hello my name is dolly would be a match but hello my name is amanda or my name is dolly would not be a match. To force them to be searched together as a phrase double quotes are required. By default Razuna uses an AND operator between keywords. So searching for hello dolly is equivalent to searching for hello AND dolly. You can override this be adding your own operator e.g. hello OR dolly which will search for terms matching either hello OR dolly i.e. hello my name is amanda or . Note that the operator must be capital case.
___
**Field Search :**
Razuna supports fielded data search. When performing a search you can either specify a field, or Razuna searches in the default fields (see above).

You can search any field by typing the field name followed by a colon ":" and then the term you are looking for.

Here are some fields that the Razuna index contains that you can search within:

id : Unique id of asset
filename : The current filename of the asset
filenameorg : The original filename the asset was uploaded with
keywords : Keywords associated with asset
description : Description associated with asset
rawmetadata : The metadata for the asset
extension : Filename extension of asset
labels : Labels associated with asset
customfieldvalue : Values in user created custom fields

If you want to find assets that have "razuna" in the "filename", you can enter:
```
filename:(razuna)
```
If you want to to search in many fields you can either use AND or OR to combine the fields, like:
```
keywords:(hello AND dolly)
```
___

**Wild Card Search :**

Razuna supports single and multiple character wildcard searches within single terms (not within phrase queries).

To perform a single character wildcard search use the "?" symbol.

To perform a multiple character wildcard search use the "*" symbol.

The single character wildcard search looks for terms that match that with the single character replaced. For example, to search for "text" or "test" you can use the search:

```
te?t
```
Multiple character wildcard searches looks for 0 or more characters. For example, to search for test, tests or tester, you can use the search:
```
test*
```
___

**Fuzzy Searches :**

Razuna supports fuzzy searches based on the Levenshtein Distance, or Edit Distance algorithm. To do a fuzzy search use the tilde, "~", symbol at the end of a Single word Term. For example to search for a term similar in spelling to "roam" use the fuzzy search:
```
roam~
```
This search will find terms like foam and roams.

A optional parameter can specify the required similarity. The value is between 0 and 1, with a value closer to 1 only terms with a higher similarity will be matched. For example:

```
roam~0.8
```

The default that is used if the parameter is not given is 0.5.
___

**Boosting a Term :**

Razuna provides the relevance level of matching documents based on the terms found. To boost a term use the caret, "^", symbol with a boost factor (a number) at the end of the term you are searching. The higher the boost factor, the more relevant the term will be.

Boosting allows you to control the relevance of a document by boosting its term. For example, if you are searching for "dam razuna" and you want the term "dam" to be more relevant boost it using the ^ symbol along with the boost factor next to the term. You would type:

```
dam^4 razuna
```

This will make documents with the term "dam" appear more relevant. You can also boost Phrase Terms as in the example:

```
"dam razuna"^4 "dam Razuna"
```

By default, the boost factor is 1. Although the boost factor must be positive, it can be less than 1 (e.g. 0.2)
___

**Boolean Operators :**

Boolean operators allow terms to be combined through logic operators. Razuna supports AND, "+", OR, NOT and "-" as Boolean operators(Note: Boolean operators must be ALL CAPS).

The OR operator is the default conjunction operator. This means that if there is no Boolean operator between two terms, the OR operator is used. The OR operator links two terms and finds a matching document if either of the terms exist in a document. This is equivalent to a union using sets. The symbol || can be used in place of the word OR.

To search for documents that contain either "dam razuna" or just "dam" use the query:

```
"dam razuna" dam
```

or

```
"dam razuna" OR dam
```
___

**AND**

The AND operator matches documents where both terms exist anywhere in the text of a single document. This is equivalent to an intersection using sets. The symbol && can be used in place of the word AND.

To search for documents that contain "dam razuna" and "DAM" use the query:

```
"dam razuna" AND "DAM"
```
___

**+**

The "" or required operator requires that the term after the "" symbol exist somewhere in a the field of a single document.

To search for documents that must contain "dam" and may contain "razuna" use the query:

```
+dam razuna
```
___

**NOT**

The NOT operator excludes documents that contain the term after NOT. This is equivalent to a difference using sets. The symbol ! can be used in place of the word NOT.

To search for documents that contain "dam razuna" but not "DAM" use the query:

```
"dam razuna" NOT "DAM"
```

Note: The NOT operator cannot be used with just one term. For example, the following search will return no results:

```
NOT "dam razuna"
```
___
**Grouping**

Razuna supports using parentheses to group clauses to form sub queries. This can be very useful if you want to control the boolean logic for a query.

To search for either "dam" or "razuna" and "DAM" use the query:

```
(dam OR razuna) AND DAM
```

This eliminates any confusion and makes sure you that website must exist and either term dam or razuna may exist.
___

**Escaping Special Characters**

Razuna supports escaping special characters that are part of the query syntax. The current list special characters are

```
+ - && || ! ( ) { } [ ] ^ " ~ * ? : \
```

To escape these character use the \ before the character. For example to search for (1+1):2 use the query:

```
\(1\+1\)\:2
```
___
### Advanced Search :

The "Advanced Search" allow us to find the file by criteria follow file format such as : Documents , Videos , Audios , Images or All of the formats. We can use file names , key words , descriptions , extension or metadata to search the files.

Please click to "Advanced Search" from Menu on top. The new windows of Advanced Search will appear for searching. After key in full the information for search, please click into "Find" button to continue.

![](img/advanced_search1.jpg)
![](img/advanced_search2.jpg)
___
### Show Basket Feature :

If you want to send some of files by email or transfer it by FTP service or download them in one moment. We can help you by "Show Basket" feature. All you can do is just click into "Put in basket" icon from the files in your folders or also your collections which you want to move them into basket for process.

![](img/basket.jpg)

After you put the data to basket , Please click to "Show Basket" link from the menu on top to show the data in Basket.

![](img/basket1.jpg)

From the Basket , user can download all the files in a zip file to local machine. Or "Save and Publish Basket" function will help you to Save basket content as a Zip , Save basket content as a Collection or Save basket content into a existing Collection. We provided some flexible choices for user when using our system. Please see the image as below :

![](img/save_basket.jpg)
___
Email Basket : 

From here , you can send data from the basket by email composer in easy way and comfortable.

![](img/send_mail_basket.jpg)
___
FTP Basket :

Our system also support user through FTP service , you can click into FTP Basket and input FTP server address , username and password to get the authentication from FTP service and allow to transfer the data from Razuna.

![](img/FTP_basket.jpg)
___

Export Metadata :

This function help you to export the metadata (Metadata summarizes basic information about data, which can make finding and working with particular instances of data easier.) of your data to a format likes :  XLS , XLSX or CSV file. You just need to choose the format and click to export button to finish.

![](img/Export_metadata_basket.jpg)
___
Remove Basket :

When user click this button , all the files in Basket will be clear from Basket.
___

### Manage Function :

From this part , users are able to create a new folder on the current level , reload the tree folder in the case if you are missing something this might help but usually not needed , Show folders from all users used to show the personal folders of your users.

![](img/Manage_add_reload_showmyfolder.jpg)

**Add folder on root level :**

In the following dialog window you are able to create a new folder on the current level. At this window , user can fill in the folder name and description. The languages for folder name and description are used in the case user want to change the default system language appearance to German , Italian or Japanese. 

After fill in step , we contine to set the permissions of folder for groups can be read , read / write or full access to this folder.

Finally we click Add button locate at bottom of dialog to finish.

![](img/Manage_add_reload_showmyfolder1.jpg)

**Reload :**
Reload the folder tree (usually not needed but if you are missing something this might help).

**Show folder from all users :**
Users can click to this part to show the personal folders to all users.
___

### How to add assets to Razuna

**Add assets from local machine :**

From your current folder on the left side, click into it and the contents in your folder will be show in main page. 

![](img/add_your_files.jpg)

To add assets , please click into "Add your Files" button and the new window appear for browse the files which you want to upload from local machine.

In this window , users click into "Add files" to browse the local files for upload and then click to "Start upload" button to load the file to Razuna System.

![](img/upload_files.jpg)

After uploading task completed , one more new window appears to require users input the metadata such as : Description , Label , Our Own Custom Field for the files which you have upload to Razuna system then click "Update Files" button to finish.

![](img/Apply_metadata_for_files.jpg)

Finally , you can see your files showing on Razuna system now.

![](img/files_show.jpg)
___

**Add assets from Server :**

For adding files from Server , all you can do is enter the corrected path to Razuna system , then checking it with Validate button to make sure the path you were entered is correct and click to Import from path to add assets from Server to Razuna System.

![](img/Add_file_from_server.jpg)
___

**Add assets from FTP :**

Please enter your FTP access information to be able to retrieve and store file from the FTP site in your system such as :

FTP server , Username , Password then Click into "Login to FTP site" button to finish.

![](img/add_file_from_ftp.jpg)
___

**Link to content :**

If you do not want to import your asset into Razuna and simply want to link to it, then add the absolute path to the asset below or enter the URL to the asset (can be on Facebook, YouTube or just about any URL that is publicly available).

Local content (on your local network) can be indexed and also converted as usual, but will not be moved to the internal Razuna structure.

![](img/Link_to_content.jpg)

___

### Menu actions in your current folder :

Our system have a Menu actions inside your current folder which you will see when open it from the image as below :

![](img/Menu_action_current_folder.jpg)

**Select All :** 

This action will allow user select all the data from the current folder for many purposes such as : Put in Basket , Create Alias , Move , Batch , Add to Existing Collection , Export Metadata or Change the Views (Thumbnail View , List View , Quick Edit View).

Or if you want to cancel the "Select All" action you can click into "Deselect All".

![](img/Select_all_menu_action_current_folder.jpg)

___

**Search within folder :**

In the case you have many files in your current folder and want to get it quickly so you can use "Search within folder" option. This option allow you filter data follow the format such as : Documents , Images , Videos and Audios or All Assets.

User just need enter the information related to the files likes : File name , Description , Label , Metadat.. etc.. and click "Find" to searching your data.

![](img/search_within_floder11.jpg)

___

**More actions :**

These actions allow user perform the tasks such as : Add Folder , Add Folder to favourites , Show assets from sub folder , Print , Rss Feed of this folder , Create a Word Document , Export Metadata , Import Metadata , Download assets in this folder.

![](img/More_action_menu.jpg)

___

**Views :**

User can change the type of views from "Thumbnail View" to "List View" or "Quick Edit View"

![](img/Views_menu.jpg)

___

### Folder Management :

There are 2 options for user want to set the "Folder subscribe" and "Folder Sharing & Settings" at the Manage Folder Menu.

![](img/Manage_folder.jpg)

**Folder subscribe :**

Subscribe to changes in folder (and its subfolders) which will be emailed to you on specifed interval.

![](img/Folder_subscribe.jpg)

**Folder Sharing & Settings :**

* Folder Settings :

In this option , Razuna system allow user do setup the properties for current folder such as : Folder name , Description , Label , Permission for groups can be access to this folder , Apply workflow to files in this folder.

![](img/folder_setting12.jpg)

* Sharing Options : 

The sharing options will be used when you share a folder all files are accessible with the same group permissions. 

![](img/Sharing_options12.jpg)

___

**Widgets :**

Widgets allow you to embed the assets in this folder/collection into any other web application, say a blog, CMS or alike.

You can create as many widgets you like, each with their own settings.

![](img/widget.jpg)

___

**Thumbnail :**

Choose Folder Thumbnail
By default the system shows a folder image for each folder. If you instead want to show your own thumbnails as the folder image, you can upload one here or choose from any existing image in this folder.

![](img/thumbnail.jpg)

___

### File Management :

When user want to change some information of their files or edit something , user just need click into any file in their current folder and the new file management window will appear.

For example , just see the image as below :

![](img/file_management.jpg)

From the sample image above , you can see the content of File Management is showing the tags including : Information , Renditions , Metadata , Comments , Versions , Sharing Options , History , Associated Collections.

____
 
**"Information Tag" :** 

User can modify the file's information likes : Filename , Description , Keywords , Labels , Expiry date. Also you can see the File size , Date added , Last modified , Located in (Folder name) , Created by (user) , ID.

Beside the showing information task , we also build an action menu at "Information Tag" with several functions such as :Put in Basket , Send via Email , Upload to FTP server , Print details , Add to Existing Collection , Move file , Move file to trash.

___

**"Rendition Tag" :**

This function will allow users to change the resolution of your image or video files and get the direct link from the preview or original file.

You can modify the resolution of files from pixel to dpi or do the opposite , or choose the suitable format files for your purpose.

After set the resolution , you click to "Convert" button to get the new resolution then you can get the direct link or get the file to local machine as well.

![](img/rendition.jpg)

___

**"Metadata Tag" :**

The Metadata Tag provide for user many of metadata standards to input such as : IPTC , XMP or Custom Metadata for process. In addition , you can copy the metadata content from this part.

![](img/metadata_file12.jpg)

___

**"Comments Tag" :**

This Tag is used by for comment to the file to marking or taking note to remember the date , tasks or anything they want.

![](img/Comments_tag.jpg)

___

**"Versions Tag" :**

In this section , user have 2 options for versions of assets.

* Upload new version :
You can replace the current original asset with a new one by choosing the file below and upload it. The current version will be saved as a version and replaced by the new asset.

* Upload old version
Uploaded new assets will be added as old versions, current original asset do not get replaced.

![](img/Version.jpg)

___

**"Sharing Options Tag" :**

Sharing Options are settings to sharing assets in the current folder. Users are able to set the file sharing options with 3 choices for each type of an asset : Downloadable , Orderable , Selected* (* Selected is valid when you use a widget. The selected asset is then used for the larger preview or for the slideshow.)

Users also can customize the sharing options and override these settings.

![](img/sharing_op1.jpg)

___

**"History Tag" :**

History is used for showing of the log of file such as : Created Date , Created Time , Description , Action , Type of file , User.

You can see or tracking the time when a file added to Razuna system and the time it was converted to other formats included its resolution information , and user who done it. 

![](img/history.jpg)

___

**"Assocciated Collections Tag" :**

One asset can be located in many collections from a system. If users want to know how many collections where storing the common file so we can use this function to check the number collections which the file is associated with.

![](img/Associate_collection.jpg)
___