**Asset API1**

> **Regarding SessionToken** : *You need to have a valid SessionToken to be able to request any method here!*

   * Asset API
       * Get asset information
           * Method
           * Input Parameter
           * Output Value
           * SOAP: Sample Request
           * REST: Sample Request
           * Sample Output
       * Get Metadata of asset
           * Input Parameter
           * Metadata parameters
           * Output Value
           * SOAP: Sample Request
           * REST: Sample Request
           * Sample Output
       * Modify metadata of asset
           * Method
           * Input Parameter
           * Metadata parameters
           * Output Value
           * SOAP: Sample Request
           * REST: Sample Request
           * Sample Output
       * Remove Asset
           * Method
           * Input Parameter
           * Output Value
           * SOAP: Sample Request
           * REST: Sample Request
           * Sample Output
       * Enable/Disable Sharing of Asset(s)
           * Method
           * Input Parameter
           * Output Value
           * SOAP: Sample Request
           * REST: Sample Request
           * Sample Output

___

**Get asset information**

*Method*

|Method Name|Available|
|-----------|---------|
|getasset|Razuna 1.4.5|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|sessiontoken|A valid sessiontoken|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|assetid|The id of the asset or a list of id's (delimited with a ",")|String|yes|108 or 108,109,etc.|
|assettype|Type of asset|String|yes|doc = Documents ; img = Images ; vid = Videos ; aud = Audios|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|Response|A result code with the status of the login. If the result is 0 the method was successful.|0|
|calledwith|The folderid you passed to this method|1|
|assets|For each asset an asset node is returned with information of the asset|see sample output|

> *Since Razuna 1.4.6 the return also contains the "RAW" metadata fields of each asset in the node <metadata>. If you want to retrieve single metadata field you can use the dedicated getmetadata() method.*

*SOAP: Sample Request*

```
folder assets = new getasset();
string assetlist = assets.getasset(sessiontoken, assetid, assettype);
```

*REST: Sample Request*

```
/global/api/asset.cfc?method=getasset&sessiontoken=54592180-7060-4D4B-BC74-2566F4B2F943
&assetid=2424HJSFSD1234&assettype=img
```

*Sample Output*

*Error rendering macro 'excerpt-include' : No link could be created for 'Folder'.*

___

**Get Metadata of asset**

> *The getasset() method already returns the description and the keyword value for each asset, thus this method only returns the associated XMP metadata values!*

> *Only PDF documents and images contain additional metadata. Obviously this method only works for "doc" and "img"!*


*Method*

|Method Name|Available|
|-----------|---------|
|getmetadata|Razuna 1.4.5|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|sessiontoken|A valid sessiontoken|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|assetid|The id of the asset or a list of id's (delimited with a ",")|String|yes|108 or 108,109,etc.|
|assettype|Type of asset|String|yes|doc = Documents (PDF) ; img = Images|
|assetmetadata|Name of metadata field to query|String|yes|headline,city,rights See the metadata field list below
	
**Metadata parameters**

*Documents*

|Metadata fields|
|---------------|
|author|
|rights|
|authorsposition|
|captionwriter|
|webstatement|
|rightsmarked|

*Images*

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


*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|Response|A result code with the status of the login. If the result is 0 the method was successful.|0|
|metadata|All the nodes of the chosen me metadata fiels.|"values"|

*SOAP: Sample Request*

```
asset getmetadata = new getmetadata();
string metadata = asset.getmetadata(sessiontoken,assetid,assettype,assetmetadata);
```

*REST: Sample Request*

```
/global/api/asset?method=getmetadata&sessiontoken=54592180-7060-4D4B-BC74-2566F4B2F943
&assetid=108&assettype=img&setmetadata=headline,city,rights
```

*Sample Output*

```
<?xml version="1.0" encoding="UTF-8"?>
<Response>
<responsecode>0</responsecode>
<asset>
<assetid>108</assetid>
<headline>New York skyline</headline>
<city>New York</city>
<rights>Royalty Free</rights>
</asset>
</Response>
```

___

**Modify metadata of asset**

*Method*

|Method Name|Available|
|-----------|---------|
|setmetadata|Razuna 1.4.5|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|sessiontoken|A valid sessiontoken|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|assetid|The id of the asset or a list of id's (delimited with a ",")|String|yes|108 or 108,109,etc.|
|assettype|Type of asset|String|yes|doc = Documents ; img = Images ; vid = Videos ; aud = Audios|
|assetmetadata||String|yes|JSON structure of metadata See the metadata field list below|

*Metadata parameters*

*You can pass all or any of the metadata fields in the assetmetadata field as a JSON structure. A example of passing the metadata for images would be (you need to serialize your array in order to pass it in a URL):*

```
[["lang_id_r","1"],["img_keywords","Razuna, Wordpress, Tomcat"],["img_description","Razuna Enterprise"],["creator","Nitai Aventaggiato"],["title","CTO"]]
```

> **Mandatory field** : *The only mandatory field you need to include is the "lang_id_r" one.*

*Videos*

|Metadata fields|
|---------------|
|vid_keywords|
|vid_description|
|vid_title|
|lang_id_r|

*Audios*

|Metadata fields|
|---------------|
|aud_keywords|
|aud_description|
|lang_id_r|

*Documents*

|Metadata fields|
|---------------|
|file_keywords|
|filedesc|
|lang_id_r|

*Images*

|Metadata fields|
|---------------|
|img_keywords|
|img_description|
|lang_id_r|

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

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|Response|A result code with the status of the login. If the result is 0 the method was successful.|0|

*SOAP: Sample Request*

```
asset asset = new asset();
string setshared = asset.setmetadata(sessiontoken,assetid,assettype,assetmetadata);
```

*REST: Sample Request*

```
/global/api/asset?method=setmetadata&sessiontoken=54592180-7060-4D4B-BC74-2566F4B2F943
&assetid=108&assettype=img&setmetadata=[["lang_id_r","1"],["img_keywords","Razuna, Wordpress, Tomcat"],["img_description","Razuna Enterprise"],["creator","Nitai Aventaggiato"],["title","CTO"]]
```

*Sample Output*

```
<?xml version="1.0" encoding="UTF-8"?>
<Response>
<responsecode>0</responsecode>
</Response>
```

___

**Remove Asset**

*Method*

|Method Name|Available|
|-----------|---------|
|remove|Razuna 1.4.6|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|sessiontoken|A valid sessiontoken|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|assetid|The id of the asset or a list of id's (delimited with a ",")|String|yes|108 or 108,109,etc.|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|Response|A result code with the status of the login. If the result is 0 the method was successful.|0|
|message|Message of the result|see sample output|

*SOAP: Sample Request*

```
asset assets = new remove();
string assetlist = assets.remove(sessiontoken, assetid);
```

*REST: Sample Request*

```
/global/api/asset.cfc?method=remove&sessiontoken=54592180-7060-4D4B-BC74-2566F4B2F943
&assetid=108,109,110
```

*Sample Output*

```
<?xml version="1.0" encoding="UTF-8"?>
<Response>
<responsecode>0</responsecode>
</Response>
```
___

**Enable/Disable Sharing of Asset(s)**

*Method*

|Method Name|Available|
|-----------|---------|
|setshared|Razuna 1.3.5|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|sessiontoken|A valid sessiontoken|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|assetid|The id of the asset or a list of id's (delimited with a ",")|String|yes|108 or 108,109,etc.|
|assettype|Type of asset|String|yes|doc = Documents ; img = Images ; vid = Videos ; aud = Audios|
|activate|Enable or disable asset|Number|yes|1 = enable ; 0 = disable|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|Response|A result code with the status of the login. If the result is 0 the method was successful.|0|

*SOAP: Sample Request*

```
asset asset = new asset();
string setshared = asset.setshared(sessiontoken,assetid,assettype,activate);
```

*REST: Sample Request*

```
/global/api/asset?method=setshared&sessiontoken=54592180-7060-4D4B-BC74-2566F4B2F943
&assetid=108&assettype=img&activate=1
```	

*Sample Output*

```
<?xml version="1.0" encoding="UTF-8"?>
<Response>
<responsecode>0</responsecode>
</Response>
```


	


	

