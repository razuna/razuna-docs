**Authentication API1**

> **Important Information about this version** : *Razuna 1.5 features a new improved version of the API! For legacy issues, we still leave this version of the API around, but developers should [develop against version 2 of the API](/api/)!* 

Authentication

   * Login
       * Method
       * Input Parameter
       * Output Value
       * SOAP: Sample Request
       * REST: Sample Request
       * Sample Output
   * Loginhost
       * Method
       * Input Parameter
       * Output Value
       * SOAP: Sample Request
       * REST: Sample Request
       * Sample Output

*Each request to the API has to be authenticated first. Without authentication your request to the API will fail. The authentication system takes in the host id and username/password to authenticate. It returns a session token that will be used for subsequent calls into the system. The SessionToken returned will expire if not used within 30 minutes.*

> **Using a Razuna.com shared account?** 

> *If you don't know the hostID you can alternatively use the loginhost method!*

**User name** : *You have to log on with a user that is either in the System administrator or Administrator Group.*

**Host ID** : *You can lookup the host id in the Administration under Hosts or if you use the Razuna Hosted service under your account page.*

___

**Login**

*The Login method is used to login to the system and generate a Session Token restricted to the caller's IP address.*

*Method*

|Method Name|
|-----------|
|login|

*Input Parameter*

|Parameter|Description|Type|Required|
|---------|-----------|----|--------|
|hostid|This is the host id under which you want to access the assets|Numeric|yes|
|user|A user in the system administrator or administrator group|String|yes|
|pass|The password of the user|String|yes|
|passhashed|Password is MD5 encrypted or not|Numeric|1 = true ; 0 = false|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|Response|A result code with the status of the login. If the result is 0 the method was successful.|0|
|SessionToken|A token that represents the logged in user.|54592180-7060-4D4B-BC74-2566F4B2F943|

*SOAP: Sample Request*

```
Authentication auth = new Authentication();
string sessionToken = auth.Login(hostid, user, pass, passhashed);
```

*REST: Sample Request*

```
/global/api/authentication.cfc?method=login&hostid=1&user=username&pass=password&passhashed=1
```

*Sample Output*

```
<?xml version="1.0" encoding="utf-8"?>
<Response>
   <ResponseCode>0</ResponseCode>
   <SessionToken>54592180-7060-4D4B-BC74-2566F4B2F943</SessionToken>
</Response>
```
___

**Loginhost**

*The Loginhost method is used to login to the system and generate a Session Token restricted to the caller's IP address.*

*Method*

|Method Name|
|-----------|
|loginhost|

*Input Parameter*

|Parameter|Description|Type|Required|
|---------|-----------|----|--------|
|hostname|Enter the name of the subdomain, example "joe.razuna.com"|String|yes|
|user|A user in the system administrator or administrator group|String|yes|
|pass|The password of the user|String|yes|
|passhashed|Password is MD5 encrypted or not|Numeric|1 = true ; 0 = false|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|Response|A result code with the status of the login. If the result is 0 the method was successful.|0|
|SessionToken|A token that represents the logged in user.|54592180-7060-4D4B-BC74-2566F4B2F943|

*SOAP: Sample Request*

```
Authentication auth = new Authentication();
string sessionToken = auth.Loginhost(hostname, user, pass, passhashed);
```

*REST: Sample Request*

```
/global/api/authentication.cfc?method=loginhost&hostname=joe.razuna.com&user=username&pass=password&passhashed=1
```

*Sample Output*

```
<?xml version="1.0" encoding="utf-8"?>
<Response>
   <ResponseCode>0</ResponseCode>
   <SessionToken>54592180-7060-4D4B-BC74-2566F4B2F943</SessionToken>
</Response>
```
	


	



