### Group API2

**Get a Group**

*Method*

|Method name|Returns|
|-----------|-------|
|getone|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|grp_id|ID of the group|String|yes|87439847981274|

*Output Value*

|Name|Description|Sample Output|Version|
|----|-----------|-------------|-------|	
|grp_id|ID of the group|87439847981274||
|grp_name|Name of the Group|MyGroup||

*REST: Sample Request*

```
/global/api2/group.cfc?method=getone&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&grp_id=87439847981274
```

*Sample Output*

```
{"columns":["grp_id","grp_name"],"data":[["87439847981274","MyGroup"]]} 
```

___

**Get all Groups**

*Method*

|Method name|Returns|
|-----------|-------|
|getall|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|

*Output Value*

|Name|Description|Sample Output|Version|
|----|-----------|-------------|-------|	
|grp_id|ID of the group|87439847981274||
|grp_name|Name of the Group|MyGroup||

*REST: Sample Request*

```
/global/api2/user.cfc?method=getall&api_key=54592180-7060-4D4B-BC74-2566F4B2F943
```

*Sample Output*

```
{"columns":["grp_id","grp_name"],"data":[["87439847981274","MyGroup"],["090798529485","Another Group"]]}
```
___

**Get Users of Groups**

*Returns the users who belong to a group.*

*Method*

|Method name|Returns|
|-----------|-------|
|getusersofgroups|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|grp_id|ID of the group|String|yes|87439847981274 You can also pass in a list of IDs separated with a "comma"|

*Output Value*

|Name|Description|Sample Output|Version|
|----|-----------|-------------|-------|
|user_first_name|First Name of the user|John|
|user_last_name|Last Name of the user|Doe|
|user_email|eMail of the user|john@doe.com|
|user_login_name|User name of the user|john|
|user_id|ID of the user|108|

*REST: Sample Request*

```
/global/api2/user.cfc?method=getusersofgroups&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&grp_id=87439847981274
```

*Sample Output*

```
{"columns":["user_id","user_login_name","user_email","user_first_name","user_last_name"],"data":[["CBCB8D26-506C-42B1-B0DA3B33ED922171","Nitai","nitai@domain.com","Nitai","Lastname"]]}
```
	
> **Output format** : *Remember you can adjust the output dynamically. The API returns JSON by default. For record sets it defaults to a ROW based set, if you need COLUMNS simply append "&__BDQUERYFORMAT=column" to your call. In case, you need JSONP you want to append "&__BDRETURNFORMAT=jsonp&callback=?". In order to retrieve XML (WDDX) you simply need to append "&__BDRETURNFORMAT=wddx".*

___

**Add a Group**

*Method*

|Method name|Returns|
|-----------|-------|
|add|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|grp_name|Name of the group|String|yes|Name of the Group|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|Response|A result code with the status. If the result is 0 the method was successful.|0|
|Message|Result message|Added successfully|

*REST: Sample Request*

```
/global/api2/user.cfc?method=add&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&grp_name=MyGroup
```

*Sample Output*

```
{["responsecode":"0","message":"Group has been added successfully","grp_id":"87439847981274"]}
```
___

**Update Group**

*Method*

|Method name|Returns|
|-----------|-------|
|update|String|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|grp_name|Name of the group|String|yes|Name of the Group|
|grp_id|ID of the group|String|yes|87439847981274|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|Response|A result code with the status. If the result is 0 the method was successful.|0|
|Message|Result message|Update successfully|

*REST: Sample Request*

```
/global/api2/group.cfc?method=update&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&grp_name=MyGroup&grp_id=87439847981274
```

*Sample Output*

```
{["responsecode":"0","message":"Group has been update successfully"]}
```

___

**Delete Group**

*Method*

|Method name|Returns|
|-----------|-------|
|delete|String|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|grp_id|ID of the group|String|yes|87439847981274|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|Response|A result code with the status. If the result is 0 the method was successful.|0|
|Message|Result message|Removed successfully|

*REST: Sample Request*

```
/global/api2/group.cfc?method=delete&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&grp_id=87439847981274
```

*Sample Output*

```
{["responsecode":"0","message":"Group has been removed successfully"]}
```