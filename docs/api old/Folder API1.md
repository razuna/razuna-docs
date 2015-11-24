**Folder API**

> **Regarding SessionToken** : *You need to have a valid SessionToken to be able to request any method here*

   * Folder API
       * Get a list of folders
           * Method
           * Input Parameter
           * Output Value
           * SOAP: Sample Request
           * REST: Sample Request
           * Sample Output
           * Sample Output for e4x
       * Get ALL folders
           * Method
           * Input Parameter
           * Output Value
           * SOAP: Sample Request
           * REST: Sample Request
           * Sample Output
           * Sample Output for e4x
       * Retrieving all assets in a folder
           * Method
           * Input Parameter
           * Output Value
           * SOAP: Sample Request
           * REST: Sample Request
           * Sample Output
       * Get Folder Information
           * Method
           * Input Parameter
           * Output Value
           * SOAP: Sample Request
           * REST: Sample Request
           * Sample Output
       * Create Folder
           * Method
           * Input Parameter
           * Output Value
           * SOAP: Sample Request
           * REST: Sample Request
           * Sample Output
       * Delete Folder
           * Method
           * Input Parameter
           * Output Value
           * SOAP: Sample Request
           * REST: Sample Request
           * Sample Output

___

**Get a list of folders**

*This method will return a list of folders on ONE level. To iterate for subfolders you will need to call this method each time. If you rather like to retrieve ALL folder and subfolders at once please take a look at the below function.*

*Method*

|Method Name|
|-----------|
|getfolders|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|sessiontoken|A valid sessiontoken|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|folderid|The ID of the folder you want to retrieve assets from.|Numeric|yes|0 = all folders on the root level|
|e4x|To return the XML in e4x format or not|Numeric|yes|0 = No ; 1 = yes|

*Output Value*

|Name|Description|Sample Output|Note|
|----|-----------|-------------|----|
|Response|A result code with the status of the login. If the result is 0 the method was successful.|0||
|listfolders|The body node of the returned list of folders|||
|folderid|ID of folder|2||
|foldername|Name of folder|Demo Folder||
|hassubfolder|Folder contains sub-folder|true or false||
|totalassets|Total of all assets in this folder|8|Razuna 1.3.5|
|totalimg|Total of all images in this folder|5|Razuna 1.3.5|
|totalvid|Total of all videos in this folder|2|Razuna 1.3.5|
|totaldoc|Total of all documents in this folder|1|Razuna 1.3.5|
|totalaud|Total of all audios in this folder|3|Razuna 1.3.5|

*SOAP: Sample Request*

```
folder assets = new folder();
string folderlist = assets.getfolders(sessiontoken, folderid, e4x);
```	

*REST: Sample Request*

```
/global/api/folder.cfc?method=getfolders&sessiontoken=54592180-7060-4D4B-BC74-2566F4B2F943
&folderid=0&e4x=0
```

*Sample Output*

```
<?xml version="1.0" encoding="UTF-8"?>
<Response>
<responsecode>0</responsecode>
<listfolders>
<folder>
<folderid>3</folderid>
<foldername>Demo Folder</foldername>
<hassubfolder>true</hassubfolder>
<totalassets>8</totalassets>
<totalimg>5</totalimg>
<totalvid>2</totalvid>
<totaldoc>1</totaldoc>
<totalaud>3</totalaud>
<folderowner>8</folderowner>
</folder>
</listfolders>
</Response>
```

*Sample Output for e4x*

```
<Response>
<responsecode>0</responsecode>
<listfolders>
<folder folderid="3" foldername="Demo Folder" hassubfolder="true" totalassets="8" totalimg="5" totalvid="2" totaldoc="1" totalaud="3" folderowner="8 />
</listfolders>
```
	
___

**Get ALL folders**

*This method will return all folders and subfolders. Please be aware that with a lot of folders this can put a strain on your Razuna server!*

*Method*

|Method Name|
|-----------|
|getfolderstree|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|sessiontoken|A valid sessiontoken|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|e4x|To return the XML in e4x format or not|Numeric|yes|0 = No ; 1 = yes|

*Output Value*

|Name|Description|Sample Output|Note|
|----|-----------|-------------|----|
|Response|A result code with the status of the login. If the result is 0 the method was successful.|0||
|listfolders|The body node of the returned list of folders|||
|folder|The root element|||
|folderid|ID of folder|2||
|foldername|Name of folder|Demo Folder||
|parentid|Parent ID of this folder|1||
|hassubfolder|Folder contains sub-folder|true or false||
|subfolder|The root element of subfolder|The subfolder element may contain all subfolders with each element of the folder||
|totalassets|Total of all assets in this folder|8|Razuna 1.3.5|
|totalimg|Total of all images in this folder|5|Razuna 1.3.5|
|totalvid|Total of all videos in this folder|2|Razuna 1.3.5|
|totaldoc|Total of all documents in this folder|1|Razuna 1.3.5|
|totalaud|Total of all audios in this folder|3|Razuna 1.3.5|
|folderowner|The userid that the folder belong to|8|Razuna 1.3.5|

*SOAP: Sample Request*

```
folder assets = new folder();
string folderlist = assets.getfolderstree(sessiontoken, e4x);
```

*REST: Sample Request*

```
/global/api/folder.cfc?method=getfolderstree&sessiontoken=54592180-7060-4D4B-BC74-2566F4B2F943
&e4x=0
```	

*Sample Output*

```
<?xml version="1.0" encoding="UTF-8"?>
<Response>
<responsecode>0</responsecode>
<listfolders>
<folder>
<folderid>3</folderid>
<foldername>Demo Folder</foldername>
<folderlevel>1</folderlevel>
<parentid>3</parentid>
<hassubfolder>true</hassubfolder>
<totalassets>8</totalassets>
<totalimg>5</totalimg>
<totalvid>2</totalvid>
<totaldoc>1</totaldoc>
<totalaud>3</totalaud>
<folderowner>8</folderowner>
<subfolder>
<folderid>12</folderid>
<foldername>A subfolder</foldername>
<folderlevel>2</folderlevel>
<parentid>3</parentid>
<hassubfolder>false</hassubfolder>
<totalassets>2</totalassets>
<totalimg>1</totalimg>
<totalvid>1</totalvid>
<totaldoc>0</totaldoc>
<totalaud>2</totalaud>
<folderowner>8</folderowner>
</subfolder>
</folder>
</listfolders>
</Response>
```

*Sample Output for e4x*

```
<Response>
<responsecode>0</responsecode>
<listfolders>
<folder folderid="3" foldername="Demo Folder" folderlevel="1" parentid="3"
 hassubfolder="true" totalassets="8" totalimg="5" totalvid="2" totaldoc="1" totalaud="3" folderowner="8">
<subfolder>
<folder folderid="12" foldername="A subfolder" folderlevel="2" parentid="3"
 hassubfolder="false" totalassets="2" totalimg="1" totalvid="1" totaldoc="0" totalaud="0" folderowner="8">
</folder>
</subfolder>
</folder>
</listfolders>
```
___

**Retrieving all assets in a folder**

*Method*

|Method Name|
|-----------|
|getassets|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|sessiontoken|A valid sessiontoken|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|folderid|The ID of the folder you want to retrieve assets from.|Numeric|yes|1|
|showsubfolders|To include assets from subfolders as well.|Numeric|yes|1 = true ; 0 = false|
|offset|This request supports paging. Enter the offset here.|Numeric|yes|0|
|maxrows|The maximum rows you want to request.|Numeric|yes|25 = show 25 assets ; 0 = show ALL assets|
|show|What kind of assets to show|String|yes|all = All assets ; img = Images only ; vid = Videos only ; doc = Documents only ; aud = Audios only|

> *The **offset** and the **maxrows** values are the same as the LIMIT option of the MySQL database. You enter the page (offset) and the amount of records you want to request. Example; There are 125 assets in a folder and you want to return 50 assets then your offset and maxrows would look like; offset=0&maxrows=50. For the next 50 assets you would use; offset=1&maxrows=50 to get to page 2 and so on.*

> **Note**: *To return **all** records, you need to give maxrows a value of 0 (zero)!*


*Output Value*

|Name|Description|Sample Output|Note|
|----|-----------|-------------|----|
|Response|A result code with the status of the login. If the result is 0 the method was successful.|0|
|totalassetscount|How many assets are in this folder|8|
|calledwith|The folderid you passed to this method|1|
|listassets|The body node of the returned list of assets||
|assets|For each asset an asset node is returned with information of the asset|see sample output|

*SOAP: Sample Request*

```
folder assets = new folder();
string assetlist = assets.getassets(sessiontoken, folderid, showsubfolders, offset, maxrows, show);
```

*REST: Sample Request*

```
/global/api/folder.cfc?method=getassets&sessiontoken=54592180-7060-4D4B-BC74-2566F4B2F943
&folderid=1&showsubfolders=0&offset=0&maxrows=25&show=all
```

*Sample Output*

```
<?xml version="1.0" encoding="UTF-8"?>
<Response>
<responsecode>0</responsecode>
<totalassetscount>6</totalassetscount>
<calledwith>1</calledwith>
<listassets>
<asset>
<kind>img</kind>
<id>67CE9D2C649D41F7B44BC169FEF9A2D0</id>
<filename>image.jpg</filename>
<extension>jpg</extension>
<description/>
<keywords>audrey hepurn,eyes,nice,image,zoe</keywords>
<url>http://razunabd.local:8080/assets/1/1/img/67CE9D2C649D41F7B44BC169FEF9A2D0/image.jpg</url>
<thumbnail>http://razunabd.local:8080/assets/1/1/img/67CE9D2C649D41F7B44BC169FEF9A2D0/thumb_67CE9D2C649D41F7B44BC169FEF9A2D0.jpg</thumbnail>
<size>65493</size>
<width>550</width>
<height>549</height>
<folderid>1</folderid>
<hasconvertedformats>true</hasconvertedformats>
<convertedformats>
<theformat>
<formatid>0211A80E35F04FF1B3AB7077F7F57605</formatid>
<formattype>gif</formattype>
<formatwidth>550</formatwidth>
<formatheight>549</formatheight>
<formatsize>225037</formatsize>
<formaturl>http://razunabd.local:8080/assets/1/1/img/0211A80E35F04FF1B3AB7077F7F57605/image.gif</formaturl>
</theformat>
<theformat>
<formatid>557B740366234D97859C1B15D180596D</formatid>
<formattype>png</formattype>
<formatwidth>550</formatwidth>
<formatheight>549</formatheight>
<formatsize>322374</formatsize>
<formaturl>http://razunabd.local:8080/assets/1/1/img/557B740366234D97859C1B15D180596D/image.png</formaturl>
</theformat>
</convertedformats>
</asset>
</listassets>
</Response>
```
___
	
**Get Folder Information**

*Method*

|Method Name|Available|
|-----------|---------|
|getfolder|Razuna 1.4.6|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|sessiontoken|A valid sessiontoken|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|folderid|The ID of the folder you want to retrieve assets from.|String|yes|1|

*Output Value*

|Name|Description|Sample Output|Note|
|----|-----------|-------------|----|	
|Response|A result code with the status of the login. If the result is 0 the method was successful.|0|
|folder_id|The folderid you passed to this method|1|
|folder_related|To which folder this folder is related to|if this is the root folder it will be the same ID as the folder id|
|folder_name|Name of this folder|Renderings|

*SOAP: Sample Request*

```
folder folder = new getfolder();
string folder = folder.getfolder(sessiontoken, folderid);
```

*REST: Sample Request*

```
/global/api/folder.cfc?method=getfolder&sessiontoken=54592180-7060-4D4B-BC74-2566F4B2F943
&folderid=1
```	

*Sample Output*

```
<?xml version="1.0" encoding="UTF-8"?>
<Response>
<responsecode>0</responsecode>
<folder_id>3</folder_id>
<folder_related>3</folder_related>
<folder_name>Demo Folder</folder_name>
</Response>
```

___

**Create Folder**

*Method*

|Method Name|Available|
|-----------|---------|
|getfolder|Razuna 1.4.6|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|sessiontoken|A valid sessiontoken|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|folderid|The ID of the folder you want to retrieve assets from.|String|yes|1|


*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|Response|A result code with the status of the login. If the result is 0 the method was successful.|0|
|folder_id|The folderid you passed to this method|1|
|folder_related|To which folder this folder is related to|if this is the root folder it will be the same ID as the folder id|
|folder_name|Name of this folder|Renderings|

*SOAP: Sample Request*

```
folder folder = new getfolder();
string folder = folder.getfolder(sessiontoken, folderid);

```

*REST: Sample Request*

```
/global/api/folder.cfc?method=getfolder&sessiontoken=54592180-7060-4D4B-BC74-2566F4B2F943
&folderid=1
```
	
*Sample Output*

```
<?xml version="1.0" encoding="UTF-8"?>
<Response>
<responsecode>0</responsecode>
<folder_id>3</folder_id>
<folder_related>3</folder_related>
<folder_name>Demo Folder</folder_name>
</Response>
```
___

**Create Folder**

*Method*

|Method Name|Available|
|-----------|---------|
|setfolder|Razuna 1.4.6|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|sessiontoken|A valid sessiontoken|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|folder_name|Name of folder|String|yes|Test Folder|
|folder_owner|The user id that this folder belongs to. If left blank then the current user is the owner.|String|yes|874329847|
|folder_related|The ID of the related folder. Important if you create a folder in a sublevel.|String|yes|You have to pass the ID of the related folder in order to make it work If the value is empty then your folder will be created in the "root"!|
|folder_collection|Is this folder a collection folder|String|yes|true ; false|
|folder_description|Description of folder|String|yes|This folder is created with the API|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|Response|A result code with the status of the login. If the result is 0 the method was successful.|0|
|folder_id|The ID of the created folder|

*SOAP: Sample Request*

```
folder folder = new setfolder();
string folder = folder.setfolder(sessiontoken, folder_name, folder_owner, folder_related, folder_collection, folder_description);
```

*REST: Sample Request*

```
/global/api/folder.cfc?method=setfolder&sessiontoken=54592180-7060-4D4B-BC74-2566F4B2F943
&folder_name=Test Folder&folder_owner=4487264&folder_related=&folder_collection=false&folder_description=This is a description
```	

> *You should always escape URL values!*

*Sample Output*

```
<?xml version="1.0" encoding="UTF-8"?>
<Response>
<responsecode>0</responsecode>
<folder_id>108</folder_id>
</Response>
```
___

**Delete Folder**

> *This method will remove the folder, any subfolders and content within! There is no to redo this action!!!*

	
*Method*

|Method Name|Available|
|-----------|---------|
|removefolder|Razuna 1.4.6|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|sessiontoken|A valid sessiontoken|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|folder_id|Name of folder|String|yes|454329579845097425097|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|Response|A result code with the status of the login. If the result is 0 the method was successful.|0|
|Message|Message|Folder and content has been successfully removed!|

*SOAP: Sample Request*

```
folder folder = new removefolder();
string folder = folder.removefolder(sessiontoken, folder_id);
```

*REST: Sample Request*

```
/global/api/folder.cfc?method=removefolder&sessiontoken=54592180-7060-4D4B-BC74-2566F4B2F943
&folder_id=948792317459725198
```	

*Sample Output*

```
<?xml version="1.0" encoding="UTF-8"?>
<Response>
<responsecode>0</responsecode>
<message>Folder has been successfully removed!</message>
</Response>
```


