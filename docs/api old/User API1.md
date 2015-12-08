**User API1**

> **Regarding SessionToken** : *You need to have a valid SessionToken to be able to request any method here plus you have to authenticate as a member of the System Administrator Group!*

> **Razuna Hosted Platform** : *Only users in the Administrator group are allowed to use these API calls.*

   * User API
       * Add a User
           * Method
           * Input Parameter
           * Output Value
           * SOAP: Sample Request
           * REST: Sample Request
           * Sample Output
       * Update User Information (as of Razuna 1.5)
           * Method
           * Input Parameter
           * Output Value
           * Userdata parameters
           * SOAP: Sample Request
           * REST: Sample Request
           * Sample Output
       * Get User Information (as of Razuna 1.3.5)
           * Method
           * Input Parameter
           * Output Value
           * SOAP: Sample Request
           * REST: Sample Request
           * Sample Output
       * Delete User (as of Razuna 1.5)
           * Method
           * Input Parameter
           * Output Value
           * SOAP: Sample Request
           * REST: Sample Request
           * Sample Output

___

**Add a User**

*Method*

|Method Name|
|-----------|
|add|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|sessiontoken|A valid sessiontoken|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|user_first_name|First Name of the user|String|yes|John|
|user_last_name|Last Name of the user|String|yes|Doe|
|user_email|eMail of the user|String|yes|john@doe.com|
|user_name|User name of the user|String|yes|john|
|user_pass|Password of the user|String|yes|john1doe (password will be MD5 hashed)|
|user_active|Activate the user|String|yes|T = true ; F= false|
|groupid|Groupid (ID of the Group you want the user to belong to)|Numeric|yes|0 = no group ; 1 = System Administrator ; 2 = Administrator ; any other number for your custom groups|

*Output Value*

|Name|Description|Sample Output|Version|
|----|-----------|-------------|-------|
|Response|A result code with the status of the login. If the result is 0 the method was successful.|0||
|Message|Reply text|User has been added successfully||
|User ID|Returns the users id|108|Razuna 1.4.5||

*SOAP: Sample Request*

```
user u = new user();
string useradd = u.add(sessiontoken, user_first_name, user_last_name, user_email, user_name, user_pass, user_active, groupid);
```
	
*REST: Sample Request*

```
/global/api/user.cfc?method=add&sessiontoken=54592180-7060-4D4B-BC74-2566F4B2F943&user_first_name=John&user_last_name=Doe
&user_email=john@doe.com&user_name=john&user_pass=john1doe&user_active=T&groupid=0
```

*Sample Output*

```
<?xml version="1.0" encoding="UTF-8"?>
<Response>
<responsecode>0</responsecode>
<Message>User has been added successfully</Message>
<userid>108</userid>
</Response>
```	

___

**Update User Information (as of Razuna 1.5)**

*Method*

|Method Name|
|-----------|
|update|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|sessiontoken|A valid sessiontoken|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|userid*|ID of user to update|String|yes|Used as a search string, can be left empty|
|userloginname*|userloginname of user to update|String|yes|Used as a search string, can be left empty|
|useremail*|eMail of user to update|String|yes|Used as a search string, can be left empty|
|userdata|A JSON string of data to update|String|yes|See below for fields in JSON|

> **Word on user fields** : *The API will do a search on the user to update. Thus provide a value for **one** (only one) of userid, userloginname or useremail fields! If the user could be found, the API will update the records, if not you will receive an error message.*
	
*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|Response|A result code with the status of the login. If the result is 0 the method was successful.|0|
|Message|Result message|Update successful|	

*Userdata parameters*

*You have to use a JSON structure to pass the user fields to be updated. Below are the fields available:*

|User fields|Note|
|-----------|----|
|user_login_name||
|user_first_name||
|user_last_name||
|user_email||
|user_pass|(you need to MD5 hash the password !!!!)|
|user_active|(T = true, F = false)|
|group_id|(provide the groupID! Leaving this field empty, will remove all group for the user)|

> *These fields can be freely used, meaning you can only update one field or as many as you need*

*SOAP: Sample Request*

```
user u = new user();
string update = u.update(sessiontoken,userid,userloginname,useremail,userdata);
```

*REST: Sample Request*

```
/global/api/user.cfc?method=update&sessiontoken=54592180-7060-4D4B-BC74-2566F4B2F943&userid=&userloginname=&useremail=user@domain.com&userdata=[["user_first_name","Joe"],["user_last_nama","Banana"]]
```

*Sample Output*

```
<?xml version="1.0" encoding="UTF-8"?>
<Response>
<responsecode>0</responsecode>
<message>Successfully update</message>
</Response>
```	

___

**Get User Information (as of Razuna 1.3.5)**

*This returns the user information of the current user logged in via the API!*

*Method*

|Method Name|
|-----------|
|getuser|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|sessiontoken|A valid sessiontoken|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|


*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|Response|A result code with the status of the login. If the result is 0 the method was successful.|0|	
|firstname|First Name of the user|John|
|lastname|Last Name of the user|Doe|
|email|eMail of the user|john@doe.com|
|username|User name of the user|john|
|userid|ID of the user|108|

*SOAP: Sample Request*

```
user u = new user();
string userget = u.getuser(sessiontoken);
```

*REST: Sample Request*

```
/global/api/user.cfc?method=getuser&sessiontoken=54592180-7060-4D4B-BC74-2566F4B2F943
```

*Sample Output*

```
<?xml version="1.0" encoding="UTF-8"?>
<Response>
<responsecode>0</responsecode>
<userid>108</userid>
<loginname>John</loginname>
<email>john@doe.com</email>
<firstname>John</firstname>
<lastname>Doe</lastname>
</Response>
```
___

**Delete User (as of Razuna 1.5)**

*Method*

|Method Name|
|-----------|
|delete|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|sessiontoken|A valid sessiontoken|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|userid*|ID of user to update|String|yes|Used as a search string, can be left empty|
|userloginname*|userloginname of user to update|String|Used as a search string, can be left empty|
|useremail*|eMail of user to update|String|yes|Used as a search string, can be left empty|

> **Word on user fields** : *The API will do a search on the user to update. Thus provide a value for **one** (only one) of userid, userloginname or useremail fields! If the user could be found, the API will delete the record, if not you will receive an error message.*

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|Response|A result code with the status of the login. If the result is 0 the method was successful.|0|
|Message|Result message|Update successful|

*SOAP: Sample Request*

```
user u = new user();
string delete = u.delete(sessiontoken,userid,userloginname,useremail);
```

*REST: Sample Request*

```
/global/api/user.cfc?method=delete&sessiontoken=54592180-7060-4D4B-BC74-2566F4B2F943&userid=&userloginname=&useremail=user@domain.com
```

*Sample Output*

```
<?xml version="1.0" encoding="UTF-8"?>
<Response>
<responsecode>0</responsecode>
<message>Successfully deleted the user</message>
</Response>
```