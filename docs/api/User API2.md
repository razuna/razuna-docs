### User API2

> **Razuna Hosted Platform** : *Only users in the Administrator group are allowed to use these API calls.*

**Add a User**

*Method*

|Method name|Returns|
|-----------|-------|
|add|String|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|user_first_name|First Name of the user|String|yes|John|
|user_last_name|Last Name of the user|String|yes|Doe|
|user_email|eMail of the user|String|yes|john@doe.com|
|user_name|User name of the user|String|yes|john|
|user_pass|Password of the user|String|yes|john1doe (password will be MD5 hashed)|
|user_active|Activate the user|String|no|T = true F= false (default)|
|groupid|Groupid (ID of the Group you want the user to belong to)|String|no|0 = no group (default) 2 = Administrator any other number for your custom groups Can not add System Administrator group (groupid 1)	|

*Output Value*

|Name|Description|Sample Output||
|----|-----------|-------------|----|
|Responsecode|A result code with the status of the login. If the result is 0 the method was successful.|0||
|Message|Reply text|User has been added successfully||
|UserID|Returns the users id|108|Razuna 1.4.5|
|apikey|Returns the api key for this user (only for users in "administrator" group)|54592180064BC7466F4B2F943| Razuna 1.5|

*REST: Sample Request*

```
/global/api2/user.cfc?method=add&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&user_first_name=John&user_last_name=Doe
&user_email=john@doe.com&user_name=john&user_pass=john1doe
```	

*Sample Output*

```
{["responsecode":"0","message":"User has been added successfully","userid":"108","apikey":"54592180064BC7466F4B2F943"]}
```
___

**Update User Information (as of Razuna 1.5)**

*Method*

|Method name|Returns|
|-----------|-------|
|update|String|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|userid*|ID of user to update|String|no|Used as a search string, can be left empty|
|userloginname*|userloginname of user to update|String|no|Used as a search string, can be left empty|
|useremail*|eMail of user to update|String|no|Used as a search string, can be left empty|
|userdata|A JSON string of data to update|String|yes|See below for fields in JSON|

> **Word on user fields** : *The API will do a search on the user to update. Thus provide a value for one (only one) of userid, userloginname or useremail fields! If the user could be found, the API will update the records, if not you will receive an error message.*

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|Response|A result code with the status of the login. If the result is 0 the method was successful.|0|
|Message|Result message|Update successful|

*Userdata parameters*

*You have to use a JSON structure to pass the user fields to be updated. Below are the fields available:*

|User field|Note|
|----------|----|
|user_login_name||
|user_first_name||
|user_last_name||
|user_email||
|user_pass|(you need to MD5 hash the password !!!!)|
|user_active|(T = true, F = false)|
|group_id|(provide the groupID! Leaving this field empty, will remove all groups for the user)|
	
> *These fields can be freely used, meaning you can combine the fields as you like*

*REST: Sample Request*

```
/global/api2/user.cfc?method=update&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&useremail=user@domain.com&userdata=[["user_first_name","Joe"],["user_last_name","Banana"]]
```

*Sample Output*

```
{["responsecode":"0","message":"User has been updated successfully","user_id":"108"]}
```	
___

**Get User Information (as of Razuna 1.3.5)**

*This returns the user information of the current user logged in via the API!*

*Method*

|Method name|Returns|
|-----------|-------|
|getuser|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|user_first_name|First Name of the user|John|
|user_last_name|Last Name of the user|Doe|
|user_email|eMail of the user|john@doe.com|
|user_login_name|User name of the user|john|
|user_id|ID of the user|108|
|user_api_key|API key for this user|54592180064BC7466F4B2F943|

*REST: Sample Request*

```
/global/api2/user.cfc?method=getuser&api_key=54592180-7060-4D4B-BC74-2566F4B2F943
```	

*Sample Output*

```
{"columns":["user_id","user_login_name","user_email","user_first_name","user_last_name"],"data":[["CBCB8D26-506C-42B1-B0DA3B33ED922171","Nitai","nitai@domain.com","Nitai","Lastname","user_api_key":"54592180064BC7466F4B2F943"]]} 
```
> **Output format** : *Remember you can adjust the output dynamically. The API returns JSON by default. For record sets it defaults to a ROW based set, if you need COLUMNS simply append "&__BDQUERYFORMAT=column" to your call. In case, you need JSONP you want to append "&__BDRETURNFORMAT=jsonp&callback=?". In order to retrieve XML (WDDX) you simply need to append "&__BDRETURNFORMAT=wddx".*

___

**Delete User (as of Razuna 1.5)**

*Method*

|Method name|Returns|
|-----------|-------|
|delete|String|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|userid*|ID of user to update|String|no|Used as a search string, can be left empty|
|userloginname*|userloginname of user to update|String|no|Used as a search string, can be left empty|
|useremail*|eMail of user to update|String|no|Used as a search string, can be left empty|

> **Word on user fields** : *The API will do a search on the user to update. Thus provide a value for one (only one) of userid, userloginname or useremail fields! If the user could be found, the API will delete the record, if not you will receive an error message.*

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|Response|A result code with the status of the login. If the result is 0 the method was successful.|0|
|Message|Result message|Update successful|

*Sample Output*

```
{["responsecode":"0","message":"User has been removed successfully","user_id":"108"]}
```