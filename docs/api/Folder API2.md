###Folder API2

**Get a list of folders**

This method will return a list of folders on ONE level. To iterate for subfolders you will need to call this method each time.
	
*Method*

|Method name|Returns|
|-----------|-------|
|getfolders|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid api key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|folderid|The ID of the folder you want to retrieve assets from.|Numeric|no|0 = all folders on the root level|
|collectionfolder|If this is a collection folder|String|no|true ; false|

*Output Value*

|Name|Description|Sample Output|Note|
|----|-----------|-------------|----|
|folder_id|ID of folder|2||
|folder_name|Name of folder|Demo Folder||
|folder_owner|ID of user that owns the folder|0CA09066-05AA-4B22-B33C1CC6EED10F3E||
|username|Name of user that owns the folder|John||
|hassubfolders|Folder contains sub-folder|true or false||
|folder_description|Folder description|Upload folder|Razuna 1.5.5 (hosted edition 12.11.2012)|
|totalassets|Total of all assets in this folder. Only populated if not a collection folder.|8|Razuna 1.3.5|
|totalimg|Total of all assets in this folder. Only populated if not a collection folder.|5|Razuna 1.3.5|
|totalvid|Total of all assets in this folder. Only populated if not a collection folder.|2|Razuna 1.3.5|
|totaldoc|Total of all assets in this folder. Only populated if not a collection folder.|1|Razuna 1.3.5|
|totalaud|Total of all assets in this folder. Only populated if not a collection folder.|3|Razuna 1.3.5|
|howmanycollections|Number of collections in collection folder. Only populated if this is a collection folder.|1||

*REST: Sample Request*

```
/global/api2/folder.cfc?method=getfolders&api_key=54592180-7060-4D4B-BC74-2566F4B2F943
```

*Sample Output*

```
{"columns":["folder_id","folder_name","folder_owner","username","hassubfolders","folder_description","totalassets","totalimg","totalvid","totaldoc","totalaud","howmanycollections"],"data":
[["E6EA9B014E6046EAA3F4390E3ED77791","Demo","1","admin","true","Contains images only",170,0,0,0,0,1]]}
```

> **Output format :** 
> *Remember you can adjust the output dynamically. The API returns JSON by default. For record sets it defaults to a ROW based set, if you need COLUMNS simply append "&__BDQUERYFORMAT=column" to your call. In case, you need JSONP you want to append "&__BDRETURNFORMAT=jsonp&callback=?". In order to retrieve XML (WDDX) you simply need to append "&__BDRETURNFORMAT=wddx".*
	
___

**Retrieving all assets in a folder**

*Method*

|Method name|Returns|
|-----------|-------|
|getassets|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api key|A valid api key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|folderid|The ID of the folder you want to retrieve assets from.|String|yes|1|
|showsubfolders|To include assets from subfolders as well.|String|no|true ; false (default)|
|show|What kind of assets to show|String|no|all = All assets (default) img = Images only vid = Videos only doc = Documents only aud = Audios only|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|totalassetscount|How many assets are in this folder|8|
|calledwith|The folderid you passed to this method|1|
|listassets|The body node of the returned list of assets||
|assets|For each asset an asset node is returned with information of the asset|see sample output|

> **Updates :**
> *As of Razuna 1.5.5 (hosted edition since 16.12.2012) the search also returns the collection id(s) the file might be in in the column "colid"*
	
*REST: Sample Request*

```
/global/api2/folder.cfc?method=getassets&api_key=54592180-7060-4D4B-BC74-2566F4B2F943
&folderid=1
```

*Sample Output*

```
{"columns":["id","filename","folder_id","extension","video_image","filename_org","kind","extension_thumb","size","width","height","description","keywords","path_to_asset","cloud_url","cloud_url_org","subassets","local_url_org","local_url_thumb","responsecode","totalassetscount","calledwith"],"data":[["5E2EB2A833C542748E314DF54AF169BD","Rodnse.jpg","33D207AF29D1447E931A8210982FC4A3","jpg","dummy","Rodnse.jpg","img","jpg","53134",412,569,"This
 is a demo","contains german u,another a in
here","33D207AF29D1447E931A8210982FC4A3/img/5E2EB2A833C542748E314DF54AF169BD","","","false","http://razunabd.local:8080//assets/1/33D207AF29D1447E931A8210982FC4A3/img/5E2EB2A833C542748E314DF54AF169BD/Rodnse.jpg","http://razunabd.local:8080//assets/1/33D207AF29D1447E931A8210982FC4A3/img/5E2EB2A833C542748E314DF54AF169BD/thumb_5E2EB2A833C542748E314DF54AF169BD.jpg","0",1,"33D207AF29D1447E931A8210982FC4A3"]]}

```
Error rendering macro 'excerpt-include' : null
___

**Get Folder Information**

*Method*

|Method name|Returns|
|-----------|-------|
|getfolder|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid api_key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943||
|folderid|The ID of the folder you want to retrieve information for|String|yes*|1|Either folderid and/or foldername must be provided.Available from Razuna version 1.6.6 onwards.|
|foldername|Full or partial name of the folder(s) you wish to retrieve information for.All folders matching the folder name criterion will be returned.|String|yes*|pictures|Either folderid and/or foldername must be provided.Available from Razuna version 1.6.6 onwards.| 

*Output Value*

|Name|Description|Sample Output|Note|
|----|-----------|-------------|----|	
|folder_id|The folderid you passed to this method|1||
|folder_related_to|To which folder this folder is related to|if this is the root folder it will be the same ID as the folder id||
|folder_name|Name of this folder|Renderings||
|folder_description|Folder description|Upload folder|Razuna 1.5.5 (hosted edition 12.11.2012)|
|folder_shared|Depicts whether folder is shared or not|true|Available from Razuna version 1.6.6 onwards.|
|group_permission|An array of groups and related permissions for folder. Groupid '0' is the 'Everybody' group.|[["73CCC1DB-C9A2-445A-B0F3CE28F8780B02","X"],["FDE74B74-D5F5-40F3-A9731BC28D14BB1D","W"],["0","R"]].|Available from Razuna version 1.6.6 onwards. |
|totalassets|Total of all assets in this folder|8||
|totalimg|Total of all assets in this folder|5||
|totalvid|Total of all assets in this folder|2||	
|totaldoc|Total of all assets in this folder|1||
|totalaud|Total of all assets in this folder|3||

*REST: Sample Request*

```
/global/api2/folder.cfc?method=getfolder&api_key=54592180-7060-4D4B-BC74-2566F4B2F943
&folderid=1
```

*Sample Output*

```
{"columns":["folder_id","folder_related_to","folder_name","totalassets","totalimg","totalvid","totaldoc","totalaud"],"data":[["33D207AF29D1447E931A8210982FC4A3","F08BA46F773647899999E80D2B52EC2C","Demo Folder",170,150,10,10,0]]} 
```

Error rendering macro 'excerpt-include' : null

___

**Create Folder**

*Method*

|Method name|Returns|
|-----------|-------|
|setfolder|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid api_key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|folder_name|Name of folder|String|yes|Test Folder|
|folder_owner|The user id that this folder belongs to. If left blank then the current user is the owner.|String|no|(if not passed uses the current user id)|
|folder_related|The ID of the related folder. Important if you create a folder in a sublevel.|String|no|1|
|folder_collection|Is this folder a collection folder|String|no|true ; false (default)|
|folder_description|Description of folder|String|no|This folder is created with the API|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|Response|A result code with the status of the login. If the result is 0 the method was successful.|0|
|folder_id|The ID of the created folder|1|

*REST: Sample Request*

```
/global/api2/folder.cfc?method=setfolder&api_key=54592180-7060-4D4B-BC74-2566F4B2F943
&folder_name=Test Folder
```

*Sample Output*	

```
{["ResponseCode":"0","folder_id":"1"]} 
```
___

**Delete Folder**

> *This method will remove the folder, any sub-folders and content within! There is no way to redo this action !*

*Method*

|Method name|Returns|
|-----------|-------|
|removefolder|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid api key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|folder_id|Name of folder|String|yes|454329579845097425097|	

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|Response|A result code with the status of the login. If the result is 0 the method was successful.|0|
|Message|Message|Folder and content has been successfully removed!|

*REST: Sample Request*

```
/global/api2/folder.cfc?method=removefolder&api_key=54592180-7060-4D4B-BC74-2566F4B2F943
&folder_id=948792317459725198
```	

*Sample Output*

```
{["ResponseCode":"0","message":"Folder and all content within has been successfully removed."]}
```
___

**Set folder permissions**

*Method*

|Method name|Returns|
|-----------|-------|
|setFolderPermissions|String|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|permissions|JSON Structure|String|yes|JSON structure. See example below|


*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|responsecode|Responsecode|0 (if successful)|
|message|Status Message|Folder permissions successfully updated|

*JSON structure*

*You pass the values for the permissions as a JSON structure. The order is:*

|Nanme|Description||
|-----|-----------|---------|
|folderid|ID of the folder||
|groupid|ID of the group|**The "EVERYBODY" group has the ID of "0" (zero)!**|
|permission|R = read only ; W = read/write ; X = full add |
	
*A example of passing the values would be (you need to serialize your array in order to pass it in a URL):*

```
[["255F307E-AE5A-4E66-AD2F6BBE81D0541C", "13E33EB4-4A82-4CF7-B1DAA549DA80E86B", "X"]]
```

*With CFML you can use the following code snippet to create the JSON (The below code will create a 2 dimensional array and using 2 groups).*

```
<cfset j = arrayNew(2)>
<cfset j[1][1] = "EA4191FB6E0F40D2AFE3ABB85E41118A">
<cfset j[1][2] = "13E33EB4-4A82-4CF7-B1DAA549DA80E86B">
<cfset j[1][3] = "X">
<cfset j[2][1] = "EA4191FB6E0F40D2AFE3ABB85E41118A">
<cfset j[2][2] = "8931CF69-7FB1-476D-9D2B00F63D9D439A">
<cfset j[2][3] = "W">
 
<cfset j = SerializeJSON(j)>
```

*REST: Sample Request*

```
/global/api2/folder.cfc?method=setFolderPermissions&api_key=CA1EBCFD45084E3991EA569DB10A29AA&permissions=[["255F307E-AE5A-4E66-AD2F6BBE81D0541C", "13E33EB4-4A82-4CF7-B1DAA549DA80E86B", "X"]]
```

*Sample Output*

```
{["responsecode":"0","message":"Folder permissions successfully added"]}
```