### Collection API2

**Get a list of Collections**

*This method will return all collections within a collection "folder". To iterate for sub-collections you will need to call this method each time.*

*Method*

|Method name|Returns|
|-----------|-------|
|getcollections|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input||
|---------|-----------|----|--------|------------|------------|
|api_key|A valid api key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943||
|folderid|The ID of the collection folder you want to retrieve collections from.|String|yes|2 As of Razuna 1.5.5 you can also pass in a list of folderid's like: 1,34,234|Razuna 1.5.5 Hosted Edition since 16.12.2012|
|released|Query collections according to released status|String|no|Empty value (default)true false|Razuna 1.5.5 Hosted Edition since 10.03.2012 |

*Output Value*

|Name|Description|Sample Output||
|----|-----------|-------------|----------|
|col_id|ID of the collection|212||
|change_date|Date of the last change to this collection|||
|col_name|Name of collection|My collection||
|collection_description|Description|My collection description|Razuna 1.5.5 (hosted edition 12.11.2012)|
|collection_keywords|Keywords|My keywords|Razuna 1.5.5 (hosted edition 16.12.2012)|
|col_released|Status of release|true|Razuna 1.5.5 (hosted edition 10.03.2012)|
|col_copied_from|If copied parent collection ID|108|Razuna 1.5.5 (hosted edition 10.03.2012)|
|totalassets|How many assets are in this collection|8||
|totalaimg|How many images are in this collection|5||
|totalavid|How many videos are in this collection|2||
|totaladoc|How many documents are in this collection|1||
|totalaud|How many audios are in this collection|3||

*REST: Sample Request*

```
/global/api2/collection.cfc?method=getcollections&api_key=54592180-7060-4D4B-BC74-2566F4B2F943
&folderid=1
```

*Sample Output*

```
{"columns":["col_id","change_date","col_name","totalimg","totalvid","totaldoc","totalaud","totalassets"],"data":[["DF45F1F8307A4B92A4EF5FB09001AFE1","January,
 30 2012 00:00:00","chakra
collection",0,0,0,0,0],["A6CE649FAA5F434EB513CA15656AB5AA","March, 15
2012 00:00:00","Marketing Material March
2012",2,1,2,0,5]]} 
```

> **Output format** :*Remember you can adjust the output dynamically. The API returns JSON by default. For record sets it defaults to a ROW based set, if you need COLUMNS simply append "&__BDQUERYFORMAT=column" to your call. In case, you need JSONP you want to append "&__BDRETURNFORMAT=jsonp&callback=?". In order to retrieve XML (WDDX) you simply need to append "&__BDRETURNFORMAT=wddx".*

___

**Retrieving all assets in a collection**

*Method*

|Method name|Returns|
|-----------|-------|
|getassets|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid api_key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|collectionid|The ID of the collection you want to retrieve assets from.|String|yes|1|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|	
|Response|A result code with the status of the login. If the result is 0 the method was successful.|0|
|calledwith|The collection id you called this method|1|
|totalassetscount|How many assets are in this folder|8|
|different value fields|Each record with is lists|see sample output|

> **Updates** : *As of Razuna 1.5.5 (hosted edition since 30.01.2013) the additional column "rendition_id" and "rendition_url" are being returned, also.*

*REST: Sample Request*

```
/global/api2/collection.cfc?method=getassets&api_key=54592180-7060-4D4B-BC74-2566F4B2F943
&collectionid=234
```

*Sample Output*

```
{"columns":["id","filename","folder_id","extension","extension_thumb","video_image","size","width","height","filename_org","kind","description","keywords","path_to_asset","cloud_url","cloud_url_org","subassets","local_url_org","local_url_thumb","responsecode","totalassetscount","calledwith","rendition_id","rendition_url"],"data":[["5DBE0927C6AA4212B0001930C0F7D7A5","01.14.12
 Affliction LA Lookbook
36475-Edit.tif","4564659C48B348C7B5DAF95AE6C3854E","jpg","jpg","dummy","65493",550,549,"2.jpg","img","","This
 is a
demo","4564659C48B348C7B5DAF95AE6C3854E/img/5DBE0927C6AA4212B0001930C0F7D7A5","","","true","http://localhost:8080/assets/1/4564659C48B348C7B5DAF95AE6C3854E/img/5DBE0927C6AA4212B0001930C0F7D7A5/2.jpg","http://localhost:8080//assets/1/4564659C48B348C7B5DAF95AE6C3854E/img/5DBE0927C6AA4212B0001930C0F7D7A5/thumb_5DBE0927C6AA4212B0001930C0F7D7A5.jpg","0",4,"c-BEF59DE2E65B4709993FDCE6C5E1D818","34941591005E44BEAE6AFE8D8EC6B89E","http://localhost:8080/assets/1/3C05DA46FA184E4F98E2A93FC7B3FFDA/img/34941591005E44BEAE6AFE8D8EC6B89E/hn2_34941591005E44BEAE6AFE8D8EC6B89E.tif"]]}
```

> **Output Format** : *Remember you can adjust the output dynamically. The API returns JSON by default. For record sets it defaults to a ROW based set, if you need COLUMNS simply append "&__BDQUERYFORMAT=column" to your call. In case, you need JSONP you want to append "&__BDRETURNFORMAT=jsonp&callback=?". In order to retrieve XML (WDDX) you simply need to append "&__BDRETURNFORMAT=wddx".*
___

**Search**

> **Availability** : *Search for collections is available as of Razuna 1.5.5 and on the Hosted Edition as of 16.12.2012! As of Razuna 1.5.5 (hosted edition since 16.12.2012) the column "colid" holds the collection ID(s) the file might be in.*

*Method*

|Method name|Returns|
|-----------|-------|
|search|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|	
|api_key|A valid api_key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|id|ID of a collection|String|no|1|
|name|Name|String|no|my collection|
|description|Description|String|no|my description|
|keyword|Keyword|String|no|my keyword|
|released||String|no|true false|

*(Name, description and keywords searches will be made as "wildcard" searches. Technically, a SQL LIKE and adding "%")*

*Output Value*

The search will return the exact output as the [getcollection() method](http://wiki.razuna.com/display/ecp/Collection+API2#CollectionAPI2-GetalistofCollections)!

*REST: Sample Request*

```
/global/api2/collection.cfc?method=search&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&name=mycol
```
> **Output format** : *Remember you can adjust the output dynamically. The API returns JSON by default. For record sets it defaults to a ROW based set, if you need COLUMNS simply append "&__BDQUERYFORMAT=column" to your call. In case, you need JSONP you want to append "&__BDRETURNFORMAT=jsonp&callback=?". In order to retrieve XML (WDDX) you simply need to append "&__BDRETURNFORMAT=wddx".*
	