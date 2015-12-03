**Razuna PHP Library (version 1)**

**Razuna PHP Library**

___

**Authentication**

To login to the Razuna system, you first have to instantiate the Razuna class with the right set of parameters (depending if you want to use the hosted razuna.com service, or a self hosted installation of Razuna), and then call the login function.

*Method*

|Method Name|
|-----------|
|constructor|

*Input Parameter (hosted razuna.com service)*

|Parameter|Description|Type|Required|
|-----------|-----------|------|------|
|hostname|Enter the name of the subdomain, example "joe.razuna.com"|String|yes|
|username|A user in the system administrator or administrator group|String|yes|
|password|The password of the user|String|yes|
|passhashed|Password is MD5 encrypted or not|Boolean|yes|
|host_type|The type of host (hosted razuna.com or not)|Razuna::HOST_TYPE_NAME|yes|

*Input Parameter (self hosted Razuna installation)*


|Parameter|Description|Type|Required|
|-----------|-----------|------|------|
|hostid|This is the host id under which you want to access the assets|Numeric|yes|
|hostname|Enter the name of the subdomain, example "joe.razuna.com"|String|yes|
|username|A user in the system administrator or administrator group|String|yes|
|password|The password of the user|String|yes|
|passhashed|Password is MD5 encrypted or not|Boolean|yes|
|host_type|The type of host (hosted razuna.com or not)|Razuna::HOST_TYPE_ID|yes|

*Method*

|Method Name|
|-----------|
|login|

*Input Parameter*

No input parameters.

*Output Value*

A session token, which you have to store somewhere. With that session token, you don't have to login on every request.	

___

**User**

**getSessionUser**

*Input Parameter*

|Parameter|Description|Type|Required|
|-----------|-----------|------|------|
|session_token|The session token of the logged in user.|String|yes|

*Output Value*

An object of RazunaUser which represents the logged in user.

___

**addUser**

*Input Parameter*

|Parameter|Description|Type|Required|
|-----------|-----------|------|------|
|user|An object of RazunaUser|RazunaUser|yes|
|session_token|The session token of the logged in user.|String|yes|

*Output Value*

true if the user was created.
An object of RazunaException is thrown if the user creation was unsuccessful.

___

**Folder**

**getFolders**

*Input Parameter*

|Parameter|Description|Type|Required|
|-----------|-----------|------|------|
|folder_id|The id of the parent folder (0 when fetching all root folders)|Numeric|yes|
|session_token|The session token of the logged in user.|String|yes|

*Output Value*

An array of RazunaFolder objects, representing the folders.

___

**getRootFolders**

Short version for getFolders(0, $session_token).

*Input Parameter*

|Parameter|Description|Type|Required|
|-----------|-----------|------|------|
|session_token|The session token of the logged in user.|String|yes|

___

**getFoldersTree**

*Input Parameter*

|Parameter|Description|Type|Required|
|-----------|-----------|------|------|
|session_token|The session token of the logged in user.|String|yes|

*Output Value*

An array of RazunaFolder objects, representing the folder tree structure.

___

**Asset**

**getAssets**

*Input Parameter*

|Parameter|Description|Type|Required|
|-----------|-----------|------|------|
|folder_id|The id of the parent folder.|Numeric|yes|
|session_token|The session token of the logged in user.|String|yes|
|show_subfolders|Also include assets of subfolders.|1 == true 0 == false|default: false|
|offset|This request supports paging. Enter the offset here.|Numeric|default: 0|
|maxrows|The maximum rows you want to request. (0 == all assets)|Numeric|default: 0|
|type|What kind of assets to show.|Razuna::ASSET_TYPE_ALL ; Razuna::ASSET_TYPE_IMAGE ; Razuna::ASSET_TYPE_VIDEO ; Razuna::ASSET_TYPE_DOCUMENT ; Razuna::ASSET_TYPE_AUDIO|default:  Razuna::ASSET_TYPE_ALL|

*Output Value*

An array of RazunaAsset objects, representing the assets.

___

**setAssetShared**

*Input Parameter*

|Parameter|Description|Type|Required|
|-----------|-----------|------|------|
|asset_id|ID of the asset.|Numeric|yes|
|type|Type of the asset.|Razuna::ASSET_TYPE_IMAGE ; Razuna::ASSET_TYPE_VIDEO ; Razuna::ASSET_TYPE_DOCUMENT ; Razuna::ASSET_TYPE_AUDIO| yes|
|activate|set shared to true or false|0 == false 1 == true|yes|

*Output value*

true if the request was successful.
An object of RazunaException is thrown if the request was unsuccessful.

___

**Hosts**

**getHosts**

*Input Parameter*

|Parameter|Description|Type|Required|
|-----------|-----------|------|------|
|session_token|The session token of the logged in user.|String|yes|


*Output Value*

An array of RazunaHost objects, representing the hosts.

___

**Search**

**searchAssets**

*Input Parameter*

|Parameter|Description|Type|Required|
|-----------|-----------|------|------|
|searchfor|The search entry. Same search syntax as in [Search and Find Assets](http://wiki.razuna.com/display/ecp/Search+and+Find+Assets) applies.|String|yes|
|session_token|The session token of the logged in user.|String|yes|
|offset|This request supports paging. Enter the offset here.|Numeric|default: 0|
|maxrows|The maximum rows you want to request. (0 == all assets)|Numeric|default: 0|
|type|What kind of assets to show.|Razuna::ASSET_TYPE_ALL ; Razuna::ASSET_TYPE_IMAGE ; Razuna::ASSET_TYPE_VIDEO ; Razuna::ASSET_TYPE_DOCUMENT ; Razuna::ASSET_TYPE_AUDIO|default: Razuna::ASSET_TYPE_ALL|
|doctype|Filters the doc type. Only applies if "show" is set to "doc"!|Razuna::DOC_TYPE_EMPTY (all types) ; Razuna::DOC_TYPE_PDF ; Razuna::DOC_TYPE_EXCEL ; Razuna::DOC_TYPE_WORD ; Razuna::DOC_TYPE_OTHER (all others)|yes|

*Output Value*

An array of RazunaAsset objects.

___

**Collection**

**getCollectionsTree**

*Input Parameter*

|Parameter|Description|Type|Required|
|-----------|-----------|------|------|
|session_token|The session token of the logged in user.|String|yes|

*Output Value*

An array of RazunaFolder objects, representing the folder tree structure for collections.

___

**getCollections**

*Input Parameter*

|Parameter|Description|Type|Required|
|-----------|-----------|------|------|
|folder_id|The id of the parent folder (0 when fetching all root folders)|Numeric|yes|
|session_token|The session token of the logged in user.|String|yes|


*Output Value*

An array of RazunaCollection objects, representing the collections.	

___

**getCollectionAssets**

*Input Parameter*

|Parameter|Description|Type|Required|
|-----------|-----------|------|------|
|collection_id|The id of the parent collection.|Numeric|yes|
|session_token|The session token of the logged in user.|String|yes|

*Output Value*

An array of RazunaAsset objects, representing the assets.

___

**Miscellaneous**

**getSessionToken - setSessionToken**

Helper methods to get and set the session token.


	






	


	




	


	

	


	

