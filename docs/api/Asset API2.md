###Asset API2

**Get asset information**

*Method*

|Method Name|Returns|
|-----------|-------|
|getasset|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|assetid|The id of the asset or a list of id's (delimited with a ",")|String|yes|108 or 108,109,etc.|
|assettype|Type of asset|String|yes|doc = Documents img = Images vid = Videos aud = Audios|

*Output Value*

|Parameter|Description|Sample Input|
|---------|-----------|------------|
|Response|A result code with the status. If the result is 0 the method was successful.|0|
|totalassetcount|Numbers of records found|8|
|calledwith|The folderid you passed to this method|108|
|assets|For each asset an asset node is returned with information of the asset|see sample output|

> Since Razuna 1.4.6 the return also contains the "RAW" metadata fields of each asset in the node <metadata>. If you want to retrieve single metadata field you can use the dedicated [getmetadata()](http://wiki.razuna.com/display/ecp/Asset+API2#AssetAPI2-getmeta) method, also.

> As of Razuna 1.5.5 (hosted edition since 16.12.2012) the search also returns the collection id(s) the file might be in in the column "colid".	

*REST: Sample Request*

```
/global/api2/asset.cfc?method=getasset&api_key=54592180-7060-4D4B-BC74-2566F4B2F943
&assetid=2424HJSFSD1234&assettype=img
```

*Sample Output*

```
{"columns":["id","filename","folder_id","extension","filename_org","extension_thumb","size","width","height","description","keywords","path_to_asset","cloud_url","cloud_url_org","metadata","hassubassets",
"local_url_org", "local_url_thumb","responsecode","totalassetscount","calledwith"],"data":[["5DBE0927C6AA4212B0001930C0F7D7A5","01.14.12 Affliction LA Lookbook 36475-Edit.tif","4564659C48B348C7B5DAF95AE6C3854E","jpg","2.jpg","jpg","65493",550,549,"","This is a demo","4564659C48B348C7B5DAF95AE6C3854E/img/5DBE0927C6AA4212B0001930C0F7D7A5","","","metadata here","true","http://localhost:8080//assets/1/4564659C48B348C7B5DAF95AE6C3854E/img/5DBE0927C6AA4212B0001930C0F7D7A5/2.jpg","http://localhost:8080//assets/1/4564659C48B348C7B5DAF95AE6C3854E/img/5DBE0927C6AA4212B0001930C0F7D7A5/thumb_5DBE0927C6AA4212B0001930C0F7D7A5.jpg","0",1,"5DBE0927C6AA4212B0001930C0F7D7A5"]]}
```

> *Output format*

> Remember you can adjust the output dynamically. The API returns JSON by default. For record sets it defaults to a ROW based set, if you need COLUMNS simply append "&__BDQUERYFORMAT=column" to your call. In case, you need JSONP you want to append "&__BDRETURNFORMAT=jsonp&callback=?". In order to retrieve XML (WDDX) you simply need to append "&__BDRETURNFORMAT=wddx".

___

**Get rendition of asset**

*Method*

|Method name|Returns|
|-----------|-------|
|getrenditions|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|Version|
|---------|-----------|----|--------|------------|-------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943||
|assetid|The id of the asset or a list of id's (delimited with a ",")|String|yes|108 or 108,109,etc.||
|assettype|Type of asset|String|yes|aud = Audios img = Images vid = Videos doc = Documents* *There are no "renditions" for documents. If you have added "additional renditions" then these will be listed!|deprecated as of 1.6.2|

*Output Value*

|Name|Description|Sample Input|
|---------|-----------|------------|
|fields with values|fields with values|see sample output|

*REST: Sample Request*

```
/global/api2/asset.cfc?method=getrenditions&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&assetid=108&assettype=img
```

*Sample Output*

```
{"COLUMNS":["type","id","width","height","path_to_asset","cloud_url_org","filename_org","extension","size","local_url_org","colorspace","xdpi","ydpi","unit","md5hash","parentid"],"DATA":[["rendition","46AAC84C9CC545F9ADCE9C9F3A640C6B",1936,1446,"CA3FE469A0B24E39B38620D104A9C0E8/img/46AAC84C9CC545F9ADCE9C9F3A640C6B","","IMG_0025_46AAC84C9CC545F9ADCE9C9F3A640C6B.png","png","5299612","http://razuna.org/assets/1/CA3FE469A0B24E39B38620D104A9C0E8/img/46AAC84C9CC545F9ADCE9C9F3A640C6B/IMG_0025_46AAC84C9CC545F9ADCE9C9F3A640C6B.png","sRGB","","","inches","3111ED783CB4207EA40B1F3AF225D6EC","42F8CDE558D5490A9ECA7C606B7B1ED0"],["rendition","D4EB0A38D2C04165A914FCE803C8A28C",1936,1446,"CA3FE469A0B24E39B38620D104A9C0E8/img/D4EB0A38D2C04165A914FCE803C8A28C","","IMG_0025_D4EB0A38D2C04165A914FCE803C8A28C.tif","tif","1592476","http://razuna.org/assets/1/CA3FE469A0B24E39B38620D104A9C0E8/img/D4EB0A38D2C04165A914FCE803C8A28C/IMG_0025_D4EB0A38D2C04165A914FCE803C8A28C.tif","sRGB","","","inches","CE68ADF6CF8659AAD6D2173F15C5DC0C","42F8CDE558D5490A9ECA7C606B7B1ED0"],["org","42F8CDE558D5490A9ECA7C606B7B1ED0",1936,2592,"CA3FE469A0B24E39B38620D104A9C0E8/img/42F8CDE558D5490A9ECA7C606B7B1ED0","","IMG_0025.jpg","jpg","2567742","http://razuna.org/assets/1/CA3FE469A0B24E39B38620D104A9C0E8/img/42F8CDE558D5490A9ECA7C606B7B1ED0/IMG_0025.jpg","sRGB","72","72","inches","08FD97C82969B24C1281A86B1E93B319",""],["thumb","42F8CDE558D5490A9ECA7C606B7B1ED0",400,299,"CA3FE469A0B24E39B38620D104A9C0E8/img/42F8CDE558D5490A9ECA7C606B7B1ED0","","IMG_0025.jpg","jpg","2567742","http://razuna.org/assets/1/CA3FE469A0B24E39B38620D104A9C0E8/img/42F8CDE558D5490A9ECA7C606B7B1ED0/thumb_42F8CDE558D5490A9ECA7C606B7B1ED0.jpg","sRGB","72","72","inches","08FD97C82969B24C1281A86B1E93B319",""],["rendition","B63F7B65DEF549B6813AE1E3D76352E2",0,0,"","http://razuna.org/images/test.png","test","img","0","http://razuna.org/images/test.png","","","","","","42F8CDE558D5490A9ECA7C606B7B1ED0"]]}
```



*Output format*

Remember you can adjust the output dynamically. The API returns JSON by default. For record sets it defaults to a ROW based set, if you need COLUMNS simply append "&__BDQUERYFORMAT=column" to your call. In case, you need JSONP you want to append "&__BDRETURNFORMAT=jsonp&callback=?". In order to retrieve XML (WDDX) you simply need to append "&__BDRETURNFORMAT=wddx".

___

**Get Metadata of asset**

> The getasset() method already returns the description and the keyword value for each asset, thus this method only returns the associated XMP metadata values! 

> Only PDF documents and images contain additional metadata. Obviously this method only works for "doc" and "img"!

*Method*	

|Method name|Returns|
|-----------|-------|
|getmetadata|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|assetid|The id of the asset or a list of id's (delimited with a ",")|String|yes|108 or 108,109,etc.|
|assettype|Type of asset|String|yes|doc = Documents (PDF) img = Images|
|assetmetadata|Name of metadata field to query|String|yes|headline,city,rights See the metadata field list below!|

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
|metadata|Your passed fields with values|"values"|

*REST: Sample Request*

```
/global/api2/asset.cfc?method=getmetadata&api_key=54592180-7060-4D4B-BC74-2566F4B2F943
&assetid=108&assettype=img&assetmetadata=headline,city,rights
```

*Sample Output*

```
{"columns":["headline","city","rights"],"data":[["Some people standing","New York","Copyright"]]} 
```

> Output Format :

> Remember you can adjust the output dynamically. The API returns JSON by default. For record sets it defaults to a ROW based set, if you need COLUMNS simply append "&__BDQUERYFORMAT=column" to your call. In case, you need JSONP you want to append "&__BDRETURNFORMAT=jsonp&callback=?". In order to retrieve XML (WDDX) you simply need to append "&__BDRETURNFORMAT=wddx".

___

**Modify metadata of asset**

*Method*

|Method name|Returns|
|-----------|-------|
|setmetadata|String|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|assetid|The id of the asset or a list of id's (delimited with a ",")|String|yes|108 or a list like 108,109,etc.|
|assettype|Type of asset|String|yes|doc = Documents img = Images vid = Videos aud = Audios|
|assetmetadata||String|yes|JSON structure of metadata See the metadata field list below|

*Metadata parameters*

You can pass all or any of the metadata fields in the assetmetadata field as a JSON structure. A example of passing the metadata for images would be (you need to serialize your array in order to pass it in a URL):

```
[["lang_id_r","1"],["file_name","new file name"],["img_keywords","Razuna, Wordpress, Tomcat"],["img_description","Razuna Enterprise"],["creator","Nitai Aventaggiato"],["title","CTO"]]
```

> Mandatory field : The only mandatory field you need to include is the "lang_id_r" one.

*Videos*

|Metadata fields||
|---------------|----------------|
|vid_keywords||
|vid_description||
|lang_id_r||
|file_name|Razuna 1.5.5 (hosted since 11.11.2012)|

*Documents*

|Metadata fields||
|---------------|----------------|
|file_keywords||
|filedesc||
|lang_id_r||
|file_name|Razuna 1.5.5 (hosted since 11.11.2012)|

*Audios*

|Metadata fields||
|---------------|----------------|
|aud_keywords||
|aud_description||
|lang_id_r||
|file_name|Razuna 1.5.5 (hosted since 11.11.2012)|

*Images*

|Metadata fields||
|---------------|----------------|
|img_keywords||
|img_description||
|lang_id_r||
|file_name|Razuna 1.5.5 (hosted since 11.11.2012)|

For images you additionally have the option to define the XMP metadata values. The following fields can be used:

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
|Response|A result code with the status. If the result is 0 the method was successful.|0|
|Message|Status Message|Metadata successfully stored|

*REST: Sample Request*

```
/global/api2/asset.cfc?method=setmetadata&api_key=54592180-7060-4D4B-BC74-2566F4B2F943
&assetid=108&assettype=img&assetmetadata=[["lang_id_r","1"],["img_keywords","Razuna, Wordpress, Tomcat"],["img_description","Razuna Enterprise"],["creator","Nitai Aventaggiato"],["title","CTO"]]
```

*Sample Output*

```
{["responsecode":"0","message":"Metadata successfully stored"]}
```

___

**Remove Asset**

This method can also be used to remove renditions. Simply pass in the id of the rendition in the assetid parameter.

*Method*


|Method name|Returns|
|-----------|-------|
|remove|String|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|assetid|The id of the asset or a list of id's (delimited with a ",")|String|yes|108 or a list like 108,109,etc.|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|Response|A result code with the status. If the result is 0 the method was successful.|0|
|message|Message of the result|see sample output|

REST: Sample Request

```
/global/api2/asset.cfc?method=remove&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&assetid=108,109,110
```

Sample Output

```
{["responsecode":"0","message":"Asset(s) have been removed successfully"]}
```

___

**Move Asset(s)**

> Availability : The "move" method is available as of Razuna 1.5.5 and on the hosted platform as of February 13th 2013.

*Method*

|Method name|Returns|
|-----------|-------|
|move|String|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|assetid|The id of the asset or a list of id's (delimited with a ",") or with the keyword "all"|String|yes|108 or a list like 108,109,etc. If you want to move ALL files in the folder you can use the keyword "all"! |
|source_folder|The folder ID where the current files are in|String|no ; required if you set assetid to "all" |2566F4B2F943|
|destination_folder|The folder ID the files should be moved to|String|yes|54592180|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|Response|A result code with the status. If the result is 0 the method was successful.|0|
|message|Message of the result|see sample output|

*REST: Sample Request*

```
/global/api2/asset.cfc?method=move&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&assetid=108,109,110&destination_folder=54592180
```

*Sample Output*

```
{["responsecode":"0","message":"Asset(s) have been moved successfully"]}
```
___

**Create renditions**

*Method*

|Method name|Returns|
|-----------|-------|
|createrenditions|String|

*Input Parameter*
	
|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|assetid|The id of the asset|String|yes|108 |
|assettype|Type of asset|String|yes|img = Images vid = Videos aud = Audios Note: There are no "renditions" for documents|
|convertdata|JSON structure of parameters for converting|String|yes|convertdata=[[["convert_to","jpg"],["convert_width_jpg","500"],["convert_height_jpg","374"],["convert_dpi_jpg",""],["convert_wm_jpg",""]]]|
|colorspace|Colorspace of asset : Images only|String	|no|Examples of Colorspace : HCL, YUV, Gray, Luv etc Reference for setting Colorspace values for an asset: [http://www.imagemagick.org/script/command-line-options.php#colorspace](http://www.imagemagick.org/script/command-line-options.php#colorspace) Note: If in the DAM administration under 'Settings' the 'Image Colorspace' is 'Set to RGB' then it will override this value. Set it back to default if you want this to take precedence.|

*Parameters for converting*

You can pass all or any of the metadata fields in the assetmetadata field as a JSON structure. A example of passing the metadata for images would be (you need to serialize your array in order to pass it in a URL):

```
convertdata=[[["convert_to","format"],["convert_width_format","value"],["convert_height_format","value"],["convert_dpi_format","value"],["convert_wm_format","value"]]]
```	

The following parameters are valid: (You need to replace the (format) with the format you want to convert to)!

|Parameter|Description|Type|Required|Application for|Comment|
|---------|-----------|----|--------|------------|----------|
|convert_to|Format to convert to|String|yes|Images, Videos, Audios|All formats are supported that you can find in the Razuna interface!|
|convert_width_(format)|Width|Number|yes|Images, Video|For no value, just leave empty|
|convert_height_(format)|Type Height|Number|yes|Images, Video|For no value, just leave empty|
|convert_dpi_(format)|DPI|Number|yes|Images|For no value, just leave empty|
|convert_wm_(format)|The ID of the Watermark template|String|yes|Images|For no value, just leave empty|
|convert_bitrate_(format)|Bitrate of Audio file|Numer|yes|Audios|All bitrates are supported as displayed in the Razuna interface. Note: For FLAC and WMV; Just pass an empty value!|

*Example: Converting to a JPG*

```
http://localhost:8080/razuna/global/api2/asset.cfc?method=createrenditions&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&assetid=E9A8DED50AAB47FDBA38D6866D1809C9&assettype=img&convertdata=[[["convert_to","jpg"],["convert_width_jpg","500"],["convert_height_jpg","374"],["convert_dpi_jpg",""],["convert_wm_jpg",""]]]
```
*Example: Converting with DPI only*

```
http://localhost:8080/razuna/global/api2/asset.cfc?method=createrenditions&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&assetid=E9A8DED50AAB47FDBA38D6866D1809C9&assettype=img&convertdata=[[["convert_to","jpg"],["convert_width_jpg",""],["convert_height_jpg",""],["convert_dpi_jpg","300"],["convert_wm_jpg",""]]]
```

*Example: Converting with a Watermark*

```
http://localhost:8080/razuna/global/api2/asset.cfc?method=createrenditions&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&assetid=E9A8DED50AAB47FDBA38D6866D1809C9&assettype=img&convertdata=[[["convert_to","jpg"],["convert_width_jpg","500"],["convert_height_jpg","374"],["convert_dpi_jpg",""],["convert_wm_jpg","11E3009FB2804C68851024C10E7EF908"]]]
```

*Example: Converting to many formats*

```
http://localhost:8080/razuna/global/api2/asset.cfc?method=createrenditions&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&assetid=E9A8DED50AAB47FDBA38D6866D1809C9&assettype=img&convertdata=

[[["convert_to","jpg"],["convert_width_jpg","400"],["convert_height_jpg","300"],["convert_dpi_jpg",""],["convert_wm_jpg",""]],
 
 
[["convert_to","png"],["convert_width_png","350"],["convert_height_png","262"],["convert_dpi_png",""],["convert_wm_png",""]],


[["convert_to","gif"],["convert_width_gif","200"],["convert_height_gif","150"],["convert_dpi_gif",""],["convert_wm_gif",""]],


[["convert_to","bmp"],["convert_width_bmp","230"],["convert_height_bmp","230"],["convert_dpi_bmp",""],["convert_wm_bmp",""]]]
```

*Example: Converting with Colorspace*

```
http://localhost:8080/razuna/global/api2/asset.cfc?method=createrenditions&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&assetid=E9A8DED50AAB47FDBA38D6866D1809C9&assettype=img&convertdata=[[["convert_to","jpg"],["convert_width_jpg","500"],["convert_height_jpg","374"],["convert_dpi_jpg",""],["convert_wm_jpg","11E3009FB2804C68851024C10E7EF908"]]]&colorspace=transparent
```

*Sample Output*

```
{["responsecode":"0","message":"Asset has been converted successfully"]}
```
___

**Regenerate asset metadata**

*Method*

|Method name|Returns|
|-----------|-------|
|regeneratemetadata|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|assetid|The id of the asset or a list of id's (delimited with a ",")|String|yes|108 or 108,109,etc.|
|assettype|Type of asset|String|yes|doc = Documents img = Images vid = Videos aud = Audios|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|Response|A result code with the status. If the result is 0 the method was successful.|0|
|Message|Success or error message if error occurred|Metadata successfully stored|

*REST: Sample Request*

```
/global/api2/asset.cfc?method=regeneratemetadata&api_key=1693DDE9404642499A677B76F4682558&assetid=FFBF081AF38C4F8F891BB453532CD08B,14497C7221A040BA92A1C1BA822369D7&assettype=img
```

*Sample Output*

```
{"responsecode":0,"message":"Metadata successfully stored"}
```

___

**Get PDF Images Information**

*Method*

|Method name|Returns|
|-----------|-------|
|getpdfimages|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|49286DAD4B464CFBB60B3742AF193758|
|assetid|The id of the asset. Must be a PDF document.|String|yes|EEE8CC192B264D65A85C08990E5E57A1|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|assetid|The original assetid passed|EEE8CC192B264D65A85C08990E5E57A1|
|name|PDF image name, corresponds to a page in the PDF|Happiness-1.jpg|
|local_directory|Directory on machine where images are stored|/Users/scott/razuna_tomcat_1_6_RC_2/tomcat/webapps/razuna/assets/1/0031D211A15B42598580B84B035EBA8C/doc/EEE8CC192B264D65A85C08990E5E57A1/razuna_pdf_images|	
|size|Size of image in bytes|81448|
|local_url_org|URL to access the image|http://localhost:8080/razuna/assets/1/0031D211A15B42598580B84B035EBA8C/doc/EEE8CC192B264D65A85C08990E5E57A1/razuna_pdf_images/Happiness-1.jpg|

*REST: Sample Request*

```
/global/api2/asset.cfc?method=getpdfimages&api_key=49286DAD4B464CFBB60B3742AF193758&assetid=EEE8CC192B264D65A85C08990E5E57A1
```

*Sample Output (No Errors)*

```
{"COLUMNS":["assetid","name","local_directory","size","local_url_org"],"DATA":[["EEE8CC192B264D65A85C08990E5E57A1","HappinesswithfinalimagesFINALF-0.jpg","/Users/bubbles/Downloads/razuna_tomcat_1_6_RC_2/tomcat/webapps/razuna/assets/1/0031D211A15B42598580B84B035EBA8C/doc/EEE8CC192B264D65A85C08990E5E57A1/razuna_pdf_images",81448,"http://localhost:8080/razuna/assets/1/0031D211A15B42598580B84B035EBA8C/doc/EEE8CC192B264D65A85C08990E5E57A1/razuna_pdf_images/HappinesswithfinalimagesFINALF-0.jpg"],["EEE8CC192B264D65A85C08990E5E57A1","HappinesswithfinalimagesFINALF-1.jpg","/Users/bubbles/Downloads/razuna_tomcat_1_6_RC_2/tomcat/webapps/razuna/assets/1/0031D211A15B42598580B84B035EBA8C/doc/EEE8CC192B264D65A85C08990E5E57A1/razuna_pdf_images",16282,"http://localhost:8080/razuna/assets/1/0031D211A15B42598580B84B035EBA8C/doc/EEE8CC192B264D65A85C08990E5E57A1/razuna_pdf_images/HappinesswithfinalimagesFINALF-1.jpg"]]}
```

*Sample Output (If Errors)*

```
{"COLUMNS":["responsecode","message"],"DATA":[["1","Asset with the given assetid could not be found. Please check assetid and try again."]]}

```