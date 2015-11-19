**Hosts API1**

> **Regarding SessionToken** : *You need to have a valid SessionToken to be able to request any method here plus you have to authenticate as a member of the System Administrator Group!*

> **Razuna SaaS Platform** : *This API is not available on the Razuna Hosted Platform*

   * Hosts API
       * Retrieving all hosts
           * Method
           * Input Parameter
           * Output Value
           * SOAP: Sample Request
           * REST: Sample Request
           * Sample Output

___

**Retrieving all hosts**

*Method*

|Method Name|
|-----------|
|gethosts|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|sessiontoken|A valid sessiontoken|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|


*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|Response|A result code with the status of the login. If the result is 0 the method was successful.|0|
|Hostid|ID of the host|1|
|Name|Name of the Host|demo|
|Path|Path to the host (relative to the web root)|demo|
|Prefix|Prefix of the database tables|demo_|

*SOAP: Sample Request*

```
hosts host = new hosts();
string gethosts = hosts.gethosts(sessiontoken);
```

*REST: Sample Request*

```
/global/api/hosts.cfc?method=gethosts&sessiontoken=54592180-7060-4D4B-BC74-2566F4B2F943
```

*Sample Output*

```
<?xml version="1.0" encoding="UTF-8"?>
<Response>
<responsecode>0</responsecode>
<host>
<id>1</id>
<name>Demo</name>
<path>demo</path>
<prefix>demo_</prefix>
</host>
</Response>
```