### Custom Fields API2

The Custom Fields API allows you to retrieve, add and get custom fields of an asset. The following methods are available: Get all custom fields , Add custom field , Get custom fields of asset , Set custom field value in bulk , Set custom field value.

**Get all custom fields**

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
|id|ID of the field|108|
|text|Text of the field|my custom field|
|type|What type the field is (text, textarea, etc.)|text|
|enabled|If the field is enabled in Razuna|T|
|show|For which asset type the field is enabled|all (default) img = Images vid = Videos aud = Audios doc = Documents users = Users |

*REST: Sample Request*

```
/global/api2/customfield.cfc?method=getall&api_key=54592180-7060-4D4B-BC74-2566F4B2F943
```

*Sample Output*

```
{"columns":["id","text","enabled","type","show"],"data":["108","my custom field","T","text","all"]]} 
```

> **Output format** : *Remember you can adjust the output dynamically. The API returns JSON by default. For record sets it defaults to a ROW based set, if you need COLUMNS simply append "&__BDQUERYFORMAT=column" to your call. In case, you need JSONP you want to append "&__BDRETURNFORMAT=jsonp&callback=?". In order to retrieve XML (WDDX) you simply need to append "&__BDRETURNFORMAT=wddx".*

___

**Add custom field**

*Method*

|Method name|Returns|
|-----------|-------|
|setfield|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|field_text|The text of the field|String|yes|my custom field|
|field_type|Type of the field|String|yes|text ; textarea ; radio (radio button) ; select (select list) ; select_multi (select multiple) as of Razuna 1.7.5|
|field_show|To what asset type should the field be enabled|String|no|all (default) ; img = Images ; vid = Videos ; aud = Audios ; doc = Documents ; users = Users |
|field_enabled|Is the field enabled within Razuna|String|no|T = yes (default) ; F = no |
|field_select_list|If your field type is a select list, enter its values here|String|no|value 1,value 2,value 3|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|responsecode|Responsecode|0 (if successful)|
|message|Status Message|Custom field successfully added|
|field_id|ID of the new custom field|109|

*REST: Sample Request*

```
/global/api2/customfield.cfc?method=setfield&api_key=CA1EBCFD45084E3991EA569DB10A29AA&field_text=location&field_type=text
```

*Sample Output*

```
{["responsecode":"0","message":"Custom field successfully added","field_id":"1110008"]}
```	
___

**Get custom fields of asset**

*Returns all custom fields from asset(s).*

*Method*

|Method name|Returns|
|-----------|-------|
|getfieldsofasset|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|asset_id|ID of the asset(s)|String|yes|108 or a list like 108,109,etc.|
|lang_id|ID of the language for the results|String|no|1 (default)|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|field_id|ID of the custom field|109090|
|field_text|Text of the custom field|location|
|field_value|Value of the custom field for this asset record|Denmark|

*REST: Sample Request*

```
/global/api2/customfield.cfc?method=getfieldsofasset&api_key=CA1EBCFD45084E3991EA569DB10A29AA&asset_id=0D624466697B4A27A498E78373AE6FF3
```

*Sample Output*

```
{"columns":["field_id","field_text","field_value"],"data":[["A7A56950-C802-4CE7-B2A36BBE5B3F454D","Hotel
Rooms",""],["237503B5-BB08-4658-8E4EFC2759847F07","photopgrapher","F"],["6BC43A50-BB0D-42C9-B8FE309678048CB0","myselect","one"]]}
```

> **Output format** : *Remember you can adjust the output dynamically. The API returns JSON by default. For record sets it defaults to a ROW based set, if you need COLUMNS simply append "&__BDQUERYFORMAT=column" to your call. In case, you need JSONP you want to append "&__BDRETURNFORMAT=jsonp&callback=?". In order to retrieve XML (WDDX) you simply need to append "&__BDRETURNFORMAT=wddx".*

___

**Set custom field value in bulk**

|Method name|Returns|
|-----------|-------|
|setfieldvaluebulk|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|field_values|JSON Structure|String|yes|JSON structure See the example below|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|responsecode|Responsecode|0 (if successful)|
|message|Status Message|Custom field values successfully added|

*JSON parameter for field_values*

*You pass the values for the custom fields as a JSON structure. The first parameter is the assetid, followed by a embedded JSON structure of the custom field ID and the custom field value. A example of passing the values would be (you need to serialize your array in order to pass it in a URL):*

```
[["1ABB08AA3B47402CB4BF1B398F4CD6F8",[["255F307E-AE5A-4E66-AD2F6BBE81D0541C","value 1"],["7FD45BCC-F3ED-4C85-8CCCF50CDCE98E8E","value 2"]]]]
```	

*In a bulk statement for many files you would simple add them to the JSON structure as in:*

```
[["1ABB08AA3B47402CB4BF1B398F4CD6F8",[["255F307E-AE5A-4E66-AD2F6BBE81D0541C","value 1"],["7FD45BCC-F3ED-4C85-8CCCF50CDCE98E8E","value 2"]]],["BB59AB4D207F41C79408E5DC04B8651A",[["FB3489CC-059E-424F-B448371E18DDE6A6","value 3"],["F72A20FE-D5EC-4CF0-98C689F6FE87CCB9","value 4"]]]]
```

*REST: Sample Request*

```
/global/api2/customfield.cfc?method=setfieldvaluebulk&api_key=CA1EBCFD45084E3991EA569DB10A29AA&field_values=[["1ABB08AA3B47402CB4BF1B398F4CD6F8",[["255F307E-AE5A-4E66-AD2F6BBE81D0541C","value 1"],["7FD45BCC-F3ED-4C85-8CCCF50CDCE98E8E","value 2"]]]]
```

*Sample Output*

```
{["responsecode":"0","message":"Custom field values successfully added"]}
```
___

**Set custom field value**

> **Bulk adding** : *You can also use the setfieldvaluebulk() method above in order to set many custom field values for many files at the same time!*

|Method name|Returns|
|-----------|-------|
|setfieldvalue|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|field_values|JSON Structure|String|yes|JSON structure of metadata See the metadata field list below To set a value for select (multiple) simply comma separate the values!|
|assetid|The id of the asset or a list of id's (delimited with a ",")|String|yes|108 or a list like 108,109,etc.|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|responsecode|Responsecode|0 (if successful)|
|message|Status Message|Custom field values successfully added|

*JSON parameter for field_values*

*You pass the values for the custom fields as a JSON structure. You also need to know the ID of the custom field. A example of passing the values would be (you need to serialize your array in order to pass it in a URL):*

```
[["255F307E-AE5A-4E66-AD2F6BBE81D0541C","value 1"],["7FD45BCC-F3ED-4C85-8CCCF50CDCE98E8E","value 2"]]
```

*REST: Sample Request*

```
/global/api2/customfield.cfc?method=setfieldvalue&api_key=CA1EBCFD45084E3991EA569DB10A29AA&assetid=0EB8E7F82A0D4A76A4AF9A72993FED5B&field_values=[["255F307E-AE5A-4E66-AD2F6BBE81D0541C","val1"],["7FD45BCC-F3ED-4C85-8CCCF50CDCE98E8E","val2"]]
```
	
*Sample Output*

```
{["responsecode":"0","message":"Custom field values successfully added"]}
```