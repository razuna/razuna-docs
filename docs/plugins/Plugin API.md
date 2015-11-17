# Plugin API

> **Plugin API** : *The plugin API is available as of Razuna 1.6.*

___

**Plugin API**

*The following API methods are available to your plugins and can be called within your CFC.*

   * Usage
   * add_action
   * del_action
   * getDatasource
   * getDatabase
   * getSchema
   * getStorage
   * getHostID
   * getHostPrefix
   * getUsers
   * getUser
   * getUsersOfGroups
   * getUploadTemplates
   * getLabels
   * getCustomFields
   * getCustomFieldsValues
   * getMyID
   * sendEmail
   * getFolderName
   * addLabels
   * execUploadTemplate
   * moveFile
   * setMetadata
   * setMetadataCustom
   * getMetadataOfFile
   * getFile

___

**Usage**

*All methods below are available in your CFC's (by the extend attribute) and should be called like:*

```
<cfset myvar = mymethod(param1="x", param2="y")>
```

___

**add_action**

*Adds the action hook into Razuna. If you want to display your template code within Razuna you need to call an action. The Plugin Hooks shows all the available actions.*

|Parameters|Required|Description|Comments|Available|
|----------|--------|-----------|--------|---------|
|pid|true|The Id of your plugin. You can get the ID programatically with getMyID().|||
|action|true|The action you want to trigger (see [Plugin Hooks](/plugins/Plugin Hooks)).|||
|comp|true|Name of your component (CFC).|||
|func|true|Name of the function to call (within the CFC you define above).|||
|args|false|Arguments to pass.|||

|Returns|
|-------|
|Nothing|

___

**del_action**

*Removes the action hook from Razuna.*

|Parameters|Required|Description|Comments|Available|
|----------|--------|-----------|--------|---------|
|pid|true|The Id of your plugin. You can get the ID programatically with getMyID().|||
|action|false|The name of the action.|||
|comp|false|Name of your component (CFC).|||
|func|false|Name of the function|||
|args|false|Arguments to pass.|||

|Returns|
|-------|
|Nothing|

*The action will be removed with a SQL query and with the parameters you pass. Example: In order to remove any action with the action name you would use this method like:*

```
<cfset del_action(pid="24zu2iucuizui34" action="on_file_add")>
```
*Please note that the "args" argument will be queried as a "wildcard" (SQL like) in order to select the actions to remove.*

___

**getDatasource**

*Returns the datasource of this Razuna instance.*

|Returns|
|-------|
|String|

*You can use the getDatasource method to dynamically get the datasource in your cfquery code. Example:*

```
<cfquery datasource="#getDatasource()#" name="myquery">...</cfquery>
```
___

**getDatabase**

*Returns the database being used. Since Razuna supports 5 different databases you sometimes need to query the database in use to adjust your SQL code.*

|Returns|Comments|
|-------|--------|
|String|h2 = The embedded H2 database (Oracle syntax support) ; oracle = Oracle ; mysql = MySQL  ; mssql = MS SQL  ; db2 = IBM DB2 |

*Example:*

```
<cfif getDatabase() EQ "mysql">...</cfid>
```
___

**getSchema**

*Returns the schema being used. For some databases (Oracle, DB2, MS SQL) Razuna places its tables into a schema. In order to query your tables correctly you need to prefix your table with the schema.*

|Returns|Comments|
|-------|--------|
|String||

___

**getStorage**

*Returns the storage mechanism being used.*

|Returns|Comments|
|-------|--------|
|String|local = Local storage ; amazon = Amazon S3 ; nirvanix = Nirvanix NAS/CDN ; akamai = Akamai NetStore |

___

**getHostID**

*Since Razuna is multi-tenant system, each tenant has its own tenant identification (hostID). You always have to query against the hostid and should always have a "host_id" column in all your tables. This allows Razuna to screen all your records in one place and is a security measurement for your customers.*

|Returns|Comments|
|-------|--------|
|String||

___

**getHostPrefix**

*Next to the HOSTID the HOSTDBPREFIX is the most important parameter. All tenants are segmented in "sharding" groups. For small deployments, this is always the same value (raz1), but for large deployments with thousands of tenants it might be that there are sharding groups deployed. To be on the save side, you **always** prefix your table queries with the hostdbprefix.*

|Returns|Comments|
|-------|--------|
|String||

```
<cfquery datasource="#getDatasource()#" name="myquery">
SELECT column
FROM #getHostPrefix()#table
WHERE host_id = #getHostID()#
</cfquery>
```
___

**getUsers**

*Gets all the users of this tenant.*

|Returns|Comments|
|-------|--------|
|Query||

___

**getUser**

*Get the detailed information from one user*

|Parameters|Required|Description|Comments|Available|
|----------|--------|-----------|--------|---------|
|user_id|true|The Id of the user.|||


|Returns|
|-------|
|Query|

___

**getUsersOfGroups**

*WIll return all users of a the given group(s).*

|Parameters|Required|Description|Comments|Available|
|----------|--------|-----------|--------|---------|
|groupid|true|The Id of the group.|You can also pass a list consisting of multiple groupids, like 108,109,110 ||

|Returns|
|-------|
|Query|

*Example:*

```
<cfset useringroup = getUsersOfGroups("108,109,110")>
```
___

**getUploadTemplates**

*Returns all available Upload Templates.*

|Returns|
|-------|
|Query|

___

**getLabels**

*Returns all available labels.*

|Returns|
|-------|
|Query|

___

**getCustomFields**

*Returns all available custom fields.*

|Returns|
|-------|
|Query|

___

**getCustomFieldsValues**

*Returns all available custom fields and the values of the fileid being passed.*

|Parameters|Required|Description|Comments|Available|
|----------|--------|-----------|--------|---------|
|fileid|true|The ID of the file.|||

|Returns|
|-------|
|Query|

___

**getMyID**

*Returns the ID of your plugin.*

|Parameters|Required|Description|Comments|Available|
|----------|--------|-----------|--------|---------|
|pluginname|true|The name of your plugin.|This should be the name of the folder you place your code in. Example "myplugin" which resides in "/razuna/plugins/myplugin" ||

|Returns|
|-------|
|Query|

*Example:*

```
<cfset myID = getMyID("myplugin")>
```

___

**sendEmail**

*Will send an eMail from Razuna.*

|Parameters|Required|Description|Comments|Available|
|----------|--------|-----------|--------|---------|
|to|false|eMail address to send eMail to|If you do **not** pass a value the eMail is being sent to the current user. Instead of using "to" you can also pass in the userid alternatively. You can use multiple addresses separated with a comma ",".||
|cc|false|eMail address to CC.|You can use multiple addresses separated with a comma ",".||
|bcc|false|eMail address to BCC|You can use multiple addresses separated with a comma ",".||
|from|false|eMail address to use for "from"|Razuna automatically uses the "from" address defined in the settings. If you want to overwrite the from email, enter an alternative address.||
|subject|false|Subject of the message|||
|message|false|Message|||
|userid|false|ID of user.|Instead of the "to" parameter you also also pass the ID of the user and it will send the message to the proper eMail address for you.||

|Returns|
|-------|
|Nothing|

___

**getFolderName**

*Returns the name of the folder.*

|Parameters|Required|Description|Comments|Available|
|----------|--------|-----------|--------|---------|
|folderid|true|The ID of the folder.|||

|Returns|
|-------|
|String|

___

**addLabels**

*Lets you assign labels to the file defined.*

|Parameters|Required|Description|Comments|Available|
|----------|--------|-----------|--------|---------|
|labelids|true|ID of the label to assign.|You can also pass in a list of labelids separated with a comma ",".||
|fileid|true|ID of the file.|||
|type|true|Type of the file.|img = images ; vid = videos ; aud = audios ; doc = all other file formats ||

|Returns|
|-------|
|Nothing|

___

**execUploadTemplate**

*Executes the Upload Template on the passed in file id.*

|Parameters|Required|Description|Comments|Available|
|----------|--------|-----------|--------|---------|
|utid|true|ID of the upload template to execute.|||
|fileid|true|ID of the file.|||
|type|true|Type of the file.|img = images ; vid = videos ; aud = audios||
|args|true|List of arguments.|||

|Returns|
|-------|
|Nothing|

___

**moveFile**

*Moves the file to the designated folder.*

|Parameters|Required|Description|Comments|Available|
|----------|--------|-----------|--------|---------|
|folderid|true|ID of the new folder.|||
|fileid|true|ID of the file.|You can also pass in a list of fileids separated with a comma ",".||
|type|true|Type of the file.|img = images ; vid = videos ; aud = audios ; doc = all other file formats||

|Returns|
|-------|
|Nothing|

___

**setMetadata**

*Applies metadata values to the file.*

|Parameters|Required|Description|Comments|Available|
|----------|--------|-----------|--------|---------|
|fileid|true|ID of the file.|You can also pass in a list of fileids separated with a comma ",".||
|type|true|Type of the file.|img = images ; vid = videos ; aud = audios ; doc = all other file formats ||
|metadata|true|Metadata|This is a list of metadata with the fieldname and value separated with a ";".||

|Returns|
|-------|
|Nothing|

*This expects metadata to be passed in as a list, separated with a ";" and the field values being separated with a ":". Example:*

```
<!--- Define list --->
<cfset metalist = "img_keywords:val1,val2;img_description:This is a nice picture of a girl">
<!--- Call method --->
<cfset setMetadata(fileid="108", type="img", metadata=metalist)>
```

**Videos**

|Metadatafields|
|--------------|
|vid_keywords|
|vid_description|

**Documents**

|Metadatafields|
|--------------|
|file_keywords|
|file_desc|

*For PDF files you additionally have the following metadata fields available:*

|Metadatafields|
|--------------|
|author|
|rights|
|authorsposition|
|captionwriter|
|webstatement|
|rightsmarked|

**Audios**

|Metadatafields|
|--------------|
|aud_keywords|
|aud_description|

**Images**

|Metadatafields|
|--------------|
|img_keywords|
|img_description|

*For images you additionally have the option to define the XMP metadata values. The following fields can be used:*

|Metadata fields|
|---------------|
|asset_type|
|subjectcode|
|creator|
|title|
|authorsposition|
|captionwriter|
|ciadrextadr|
|category|
|supplementalcategories|
|urgency|
|description|
|ciadrcity|
|ciadrctry|
|location|
|ciadrpcode|
|ciemailwork|
|ciurlwork|
|citelwork|
|intellectualgenre|
|instructions|
|source|
|usageterms|
|copyrightstatus|
|transmissionreference|
|webstatement|
|headline|
|datecreated|
|city|
|ciadrregion|
|country|
|countrycode|
|scene|
|state|
|credit|
|rights|

___

**setMetadataCustom**

*Applies custom metadata value to the file.*

|Parameters|Required|Description|Comments|Available|
|----------|--------|-----------|--------|---------|
|fileid|true|ID of the file.|You can also pass in a list of fileids separated with a comma ",".||
|type|true|Type of the file.|img = images ; vid = videos ; aud = audios ; doc = all other file formats ||
|metadata|true|Metadata|This is a list of metadata with the custom fields ID and value separated with a ";".|

|Returns|
|-------|
|Nothing|

*This expects metadata to be passed in as a list, separated with a ";" and the field values being separated with a ":". Example:*

```
<!--- Custom Field ID --->
<cfset fieldid = "ABC999">
<!--- Define list --->
<cfset metalist = "#fieldid#:val1;">
<!--- Call method --->
<cfset setMetadataCustom(fileid="108", type="img", metadata=metalist)>
```
___

**getMetadataOfFile**

*Gets the description, keywords and RAW metadata from the file. Will additionally return all the XMP metadata for images and PDF files.*

|Parameters|Required|Description|Comments|Available|
|----------|--------|-----------|--------|---------|
|fileid|true|ID of the file.|You can also pass in a list of fileids separated with a comma ",".||
|type|true|Type of the file.|img = images ; vid = videos ; aud = audios ; doc = all other file formats ||

|Returns|
|-------|
|Query|

___

**getFile**

*Gets the file record(s)*

|Parameters|Required|Description|Comments|Available|
|----------|--------|-----------|--------|---------|
|fileid|true|ID of the file.|You can also pass in a list of fileids separated with a comma ",".||

|Returns|
|-------|
|Query|


