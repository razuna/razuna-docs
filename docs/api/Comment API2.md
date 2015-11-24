### Comment API2
	
*The Comment API allows you to add, modify and remove comments in your system. The following methods are available: Get all , Get one , Add or Update , Remove*

**Get all**

*Returns all comments from the passed ID.*

*Method*

|Method name|Returns|
|-----------|-------|
|getall|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|id|Valid file or collection ID|String|yes|7859437598-2345-2345|
|type|the "file" type|String|yes|col = collection img = images vid = videos aud = audios doc = documents|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|com_id|ID of the comment|1|
|com_text|comment|This is a comment|
|com_date|Date when the comment has been added|2012-11-10 17:00:00|
|user_login_name|Login name of user|Martin|
|user_first_name|First name of user|Martin|
|user_last_name|Last name of user|Master|

*REST: Sample Request*

```
/global/api2/comment.cfc?method=getall&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&id=7859437598-2345-2345&type=vid
```

*Sample Output*

```
{"COLUMNS":["com_id","com_text","com_date","user_login_name","user_first_name","user_last_name"],"DATA":[["F1E00574-2874-4B5E-A82BA6CC7D45856A","A
 new comment form the API","December, 13 2012 17:39:04","nitai","test","test"]]}
```

> **Output format** : *Remember you can adjust the output dynamically. The API returns JSON by default. For record sets it defaults to a ROW based set, if you need COLUMNS simply append "&__BDQUERYFORMAT=column" to your call. In case, you need JSONP you want to append "&__BDRETURNFORMAT=jsonp&callback=?". In order to retrieve XML (WDDX) you simply need to append "&__BDRETURNFORMAT=wddx".*

___

**Get one**

*Method*

|Method name|Returns|
|-----------|-------|
|get|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|id|Valid file or collection ID|String|yes|7859437598-2345-2345|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|com_id|ID of the comment|1|
|com_text|comment|This is a comment|
|com_date|Date when the comment has been added|2012-11-10 17:00:00|
|user_login_name|Login name of user|Martin|
|user_first_name|First name of user|Martin|
|user_last_name|Last name of user|Master|

*REST: Sample Request*

```
/global/api2/comment.cfc?method=get&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&id=7859437598-2345-2345
```

*Sample Output*

```
{"COLUMNS":["com_id","com_text","com_date","user_login_name","user_first_name","user_last_name"],"DATA":[["F1E00574-2874-4B5E-A82BA6CC7D45856A","A
 new comment form the API","December, 13 2012 17:39:04","nitai","test","test"]]}
```

> **Output format** : *Remember you can adjust the output dynamically. The API returns JSON by default. For record sets it defaults to a ROW based set, if you need COLUMNS simply append "&__BDQUERYFORMAT=column" to your call. In case, you need JSONP you want to append "&__BDRETURNFORMAT=jsonp&callback=?". In order to retrieve XML (WDDX) you simply need to append "&__BDRETURNFORMAT=wddx".*

___

**Add or update**

*Method*

|Method name|Returns|
|-----------|-------|
|set|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|id|ID of the comment (Provide the ID only if you want to update. DON'T pass any value and the comment will be added!)|String|no|1110008|
|id_related|ID of the collection of file this comment relates to|String|yes|54592180|
|comment|Comment|String|yes|pictures|
|type|the "file" type|String|yes|col = collection ; img = images ; vid = videos ; aud = audios ; doc = documents|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|responsecode|A response number|0 = success|
|message|Status of operation|Comment added/updated successfully|
|id|Either the new comment id or the existing ID (on update)|1110008|

*REST: Sample Request*

```
/global/api2/comment.cfc?method=set&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&id=1110008&id_related=54592180&comment=My update form the API&type=img
```

*Sample Output*

```
{["responsecode":"0","message":"Comment updated successfully","id":"1110008"]}
```	
___

**Remove**

*Method*

|Method name|Returns|
|-----------|-------|
|remove|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|id|ID of the comment|String|yes|108|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|responsecode|A response number|0 = success|
|message|Status of operation|Comment removed|

*REST: Sample Request*

```
/global/api2/comment.cfc?method=remove&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&id=108
```

*Sample Output*

```
{["responsecode":"0","message":"Comment removed"]}
```