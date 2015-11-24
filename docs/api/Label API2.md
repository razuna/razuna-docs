### Label API2

The Label API allows you to add, modify and remove labels in your system. Furthermore you can label your assets or remove labels from the asset. The following methods are available: Get all labels ; Get one label ; Add or update a label ; Remove a label ; Add labels to an asset ; Remove labels from an asset ; Get label of asset ; Get asset of label ; Search for label(s).

**Get all labels**

*Method*

|Method name|Returns|
|-----------|-------|
|getall|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|	
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|label_id|ID of the label|1|
|label_text|Text of the label itself|pictures|
|label_path|Path of the label, each level is separated with a "/"|pictures/color|

*REST: Sample Request*

```
/global/api2/label.cfc?method=getall&api_key=54592180-7060-4D4B-BC74-2566F4B2F943
```

*Sample Output*

```
{"columns":["label_id","label_text","label_path"],"data":["1","pictures","pictures/color"]]} 
```

> **Output format** : *Remember you can adjust the output dynamically. The API returns JSON by default. For record sets it defaults to a ROW based set, if you need COLUMNS simply append "&__BDQUERYFORMAT=column" to your call. In case, you need JSONP you want to append "&__BDRETURNFORMAT=jsonp&callback=?". In order to retrieve XML (WDDX) you simply need to append "&__BDRETURNFORMAT=wddx".*

___

**Get one label**

*Method*

|Method name|Returns|
|-----------|-------|
|getlabel|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|label_id|ID of the label|String|yes|108 or as a list 108,109|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|label_id|ID of the label|1|
|label_text|Text of the label itself|pictures|
|label_path|Path of the label, each level is separated with a "/"|pictures/color|

*REST: Sample Request*

```
/global/api2/label.cfc?method=getlabel&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&label_id=108
```

*Sample Output*

```
{"columns":["label_id","label_text","label_path"],"data":["1","pictures","pictures/color"]]}
```

> **Outout format** : *Remember you can adjust the output dynamically. The API returns JSON by default. For record sets it defaults to a ROW based set, if you need COLUMNS simply append "&__BDQUERYFORMAT=column" to your call. In case, you need JSONP you want to append "&__BDRETURNFORMAT=jsonp&callback=?". In order to retrieve XML (WDDX) you simply need to append "&__BDRETURNFORMAT=wddx".*

___

**Add or update a label**

*Method*

|Method name|Returns|
|-----------|-------|
|setlabel|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|label_id|ID of the label (Provide an label ID if you want to update the label, else DON'T pass any value and the label will be added!)|String|no|108|
|label_text|Text of the label|String|yes|pictures|
|label_parent|The parent label to nest the label|String|no|107|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|responsecode|A response number|0 = success|
|message|Status of operation|Label updated successfully|
|label_id|The label id. If you create a new label, the ID of the label, else the ID you're passing|1110008|

*REST: Sample Request*

```
/global/api2/label.cfc?method=setlabel&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&label_text=painting
```

*Sample Output*

```
{["responsecode":"0","message":"Label added successfully","label_id":"1110008"]}
```
___

**Remove a label**

*Method*

|Method name|Returns|
|-----------|-------|
|remove|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|label_id|ID(s) of the label to remove|String|yes|108 or as a list 108,109|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|responsecode|A response number|0|
|message|Status of operation|Label(s) removed|

*REST: Sample Request*

```
/global/api2/label.cfc?method=remove&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&label=108
```

*Sample Output*

```
{["responsecode":"0","message":"Label(s) removed"]}
```
___

**Add labels to an asset**

Method*

|Method name|Returns|
|-----------|-------|
|setassetlabel|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|label_id|ID of the label|String|yes|108 or a list of IDs 108,109|
|asset_id|ID of the asset|String|yes|129844|
|asset_type|Type of asset|String|yes|img = images vid = videos aud = audios doc = documents folder = folders collection = collection |
|append|If set to true it will append to existing labels, else set to false to overwrite|String|no|true (default) false (all labels will be replaced with these ones)|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|responsecode|A response number|0 = success|
|message|Status of operation|Label(s) added|

*REST: Sample Request*

```
{["responsecode":"0","message":"label has been assed to the asset successfully"]}
```
___

*Remove labels from an asset*

*Method*

|Method name|Returns|
|-----------|-------|
|removeassetlabel|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|label_id|ID(s) of the label to remove|String|yes|108 or as a list 108,109|
|asset_id|ID of the asset|String|yes|1989|	

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|responsecode|A response number|0 = success|
|message|Status of operation|Label(s) removed|

*REST: Sample Request*

```
/global/api2/label.cfc?method=removeassetlabel&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&label_id=108&asset_id=1989
```

*Sample Output*

```
{["responsecode":"0","message":"Label(s) has been removed from the asset successfully]} 
```
___

**Get label of asset**

*Returns all labels of an asset.*

*Method*

|Method name|Returns|
|-----------|-------|
|getlabelofasset|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|asset_id|ID of the asset|String|yes|108 or as a list 108,109|
|asset_type|Type of asset to query|String|yes|img = images doc = documents vid = videos aud = audios folder = folders collection = collections |

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|label_id|ID of the label|1|
|label_text|Text of the label itself|pictures|
|label_path|Path of the label, each level is separated with a "/"|pictures/color|

*REST: Sample Request*

```
/global/api2/label.cfc?method=getlabelofasset&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&asset_id=108&asset_type=img
```

*Sample Output*

```
{"columns":["label_id","label_text","label_path"],"data":["1","pictures","pictures/color"]]}
```

> **Output format** : *Remember you can adjust the output dynamically. The API returns JSON by default. For record sets it defaults to a ROW based set, if you need COLUMNS simply append "&__BDQUERYFORMAT=column" to your call. In case, you need JSONP you want to append "&__BDRETURNFORMAT=jsonp&callback=?". In order to retrieve XML (WDDX) you simply need to append "&__BDRETURNFORMAT=wddx".*

___

**Get asset of label**

*Returns all assets with the given label_id.*

*Method*

|Method name|Returns|
|-----------|-------|
|getassetoflabel|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|label_id|Label ID|String|yes|108|
|label_type|From which label type to return records|String|no|assets (default) folders collections |

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|Columns|Different columns|see sample output|

*REST: Sample Request*

```
/global/api2/label.cfc?method=getassetoflabel&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&label_id=108
```

*Sample Output*

```
{"columns":["id","filename","folder_id_r","ext","filename_org","kind","is_available","date_create","date_change","link_kind","link_path_url","path_to_asset","cloud_url"],"data":[["5CACD8076F2A41909790DF9C4BCBE60B","IMG_0903.jpg","E6EA9B014E6046EAA3F4390E3ED77791","jpg","IMG_0903.jpg","img","1","April,
 23 2012 19:12:55","March, 26 2012
00:00:00","","/Users/nitai/Documents/workspace/razuna/raz1/dam/incoming/api5CACD8076F2A41909790DF9C4BCBE60B","E6EA9B014E6046EAA3F4390E3ED77791/img/5CACD8076F2A41909790DF9C4BCBE60B",""]]}
```

> **Output format** : *Remember you can adjust the output dynamically. The API returns JSON by default. For record sets it defaults to a ROW based set, if you need COLUMNS simply append "&__BDQUERYFORMAT=column" to your call. In case, you need JSONP you want to append "&__BDRETURNFORMAT=jsonp&callback=?". In order to retrieve XML (WDDX) you simply need to append "&__BDRETURNFORMAT=wddx".*

___

**Search for label(s)**

> **Availability** : *This API method is available in release 1.6.2 and above*

*Method*

|Method name|Returns|
|-----------|-------|
|searchlabel|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|searchfor|Label(s) to search for|String|yes|pictures|
|overridemax|The search limits the # of records returned to 1000. If you wish to return all records you can use this parameter to override the limit e.g. &overridemax=1. Doing so may use up server resources so caution should be used with large record sets. |Numeric|no|1|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|label_id|ID of the label|1|
|label_text|Text of the label itself|pictures|
|label_path|Path of the label, each level is separated with a "/"|

*REST: Sample Request*

```
/global/api2/label.cfc?method=searchlabel&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&searchfor=pictures
```

*Sample Output*

```
{"columns":["label_id","label_text","label_path"],"data":["1","pictures","pictures/color"]]} 
```