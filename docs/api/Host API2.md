### Hosts API2

**Retrieving all hosts**
	
*Method*

|Method name|Returns|
|-----------|-------|
|gethosts|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|


*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|host_id|ID of the host|1|
|host_name|Name of the Host|raz1|
|host_path|Path to the host (relative to the web root)|raz1|
|host_db_prefix|Prefix of the database tables|raz1_|
|host_shard_group|The sharding group of this host|shard1|

*REST: Sample Request*

```
/global/api2/hosts.cfc?method=gethosts&api_key=54592180-7060-4D4B-BC74-2566F4B2F943		
```

> **Output format** : *Remember you can adjust the output dynamically. The API returns JSON by default. For record sets it defaults to a ROW based set, if you need COLUMNS simply append "&__BDQUERYFORMAT=column" to your call. In case, you need JSONP you want to append "&__BDRETURNFORMAT=jsonp&callback=?". In order to retrieve XML (WDDX) you simply need to append "&__BDRETURNFORMAT=wddx".*

___

**Get size of host**

> **Availability** : *This API method is available in release 1.6.2 and above*

*Method*

|Method name|Returns|
|-----------|-------|
|gethostsize|String|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|host_id|A valid HostID|Integer|no|1|

*Note: Just passing the api key only will return all the hosts with the size!*

*Output Value*

```
{"hostid":"hostsize"}
```

*REST: Sample Request*

```
/global/api2/hosts.cfc?method=gethostsize&api_key=54592180-7060-4D4B-BC74-2566F4B2F943
```

*Sample Output*

```
{"1":"283M"}
```