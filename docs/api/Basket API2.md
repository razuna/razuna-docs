### Basket API2

The basket API allows a developer to use Razuna for storing files in a temporary location on the Razuna server. This gives you the power of a shopping cart like feature. The following methods are available:

* How does it works
* Add files to basket
* Show basket
* Delete all files in basket
* Delete item in basket
* Download basket

___

**How does it works**

*In order to store files in the basket, you need to generate a "basket_id" in your system. This can be any kind of number, string, etc. Simply make sure you give each user of your website a unique number. Then simply pass this basket_id to every request on your site (so users can browse your site without loosing their basket). With this basket_id you also query the basket API. You also need to have an API KEY to use this API.*

___

**Add files to basket**

*Adds any kind of file to the basket.*

*Method*

|Method name|Returns|
|-----------|-------|
|addToBasket|String|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|basket_id|Basket Id|String|yes|7859437598-2345-2345|
|asset_id|Valid ID of an asset in Razuna|String|yes|523908044-4355-4R5T-B67B-55TG767U875|
|asset_type|Original or thumbnail|String|no|defaults to original file. If you want to add the thumbnail to a basket use "thumb" .Only applies to images!|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|responsecode|A response number|0 = success|
|message|Status of operation|File has been added to the basket|

*REST: Sample Request*

```
/global/api2/basket.cfc?method=addToBasket&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&basket_id=7859437598-2345-2345&asset_id=523908044-4355-4R5T-B67B-55TG767U875
```
	
*Sample Output*

```
{["responsecode":"0","message":"File has been added to the basket"]}
```

> **Output format** : *Remember you can adjust the output dynamically. The API returns JSON by default. For record sets it defaults to a ROW based set, if you need COLUMNS simply append "&__BDQUERYFORMAT=column" to your call. In case, you need JSONP you want to append "&__BDRETURNFORMAT=jsonp&callback=?". In order to retrieve XML (WDDX) you simply need to append "&__BDRETURNFORMAT=wddx".*

___

**Show basket**

*Method*

|Method name|Returns|
|-----------|-------|
|showBasket|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|basket_id|Basket Id|String|yes|7859437598-2345-2345|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|asset_id|The asset id|108|
|asset_type|By default "org" (original) else "thumb" (thumbnail)|org|

*REST: Sample Request*

```
/global/api2/basket.cfc?method=showBasket&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&basket_id=7859437598-2345-2345
```

*Sample Output*

```
{"COLUMNS":["asset_id","asset_type"],"DATA":[["F1E00574-2874-4B5E-A82BA6CC7D45856A","org"]]}
```

> **Output format** : *Remember you can adjust the output dynamically. The API returns JSON by default. For record sets it defaults to a ROW based set, if you need COLUMNS simply append "&__BDQUERYFORMAT=column" to your call. In case, you need JSONP you want to append "&__BDRETURNFORMAT=jsonp&callback=?". In order to retrieve XML (WDDX) you simply need to append "&__BDRETURNFORMAT=wddx".*

___

**Delete all files in basket**

*Method*

|Method name|Returns|
|-----------|-------|
|deleteBasket|String|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|basket_id|Basket ID|String|ywa|7859437598-2345-2345|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|responsecode|A response number|0 = success|
|message|Status of operation|All files in your basket have been removed|

*REST: Sample Request*

```
/global/api2/basket.cfc?method=deleteBasket&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&basket_id=7859437598-2345-2345
```

*Sample Output*

```
{["responsecode":"0","message":"All files in your basket have been removed"]}
```
___

**Delete item in basket**

*Method*

|Method name|Returns|
|-----------|-------|
|deleteItemInBasket|String|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|basket_id|Basket ID of the comment|String|yes|7859437598-2345-2345|
|asset_id|Asset ID|String|yes|108|
|asset_type|Type of asset|String|no|"org" (default) ; "thumb" for thumbnail (only applies to images)|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|responsecode|A response number|0 = success|
|message|Status of operation|File have been removed from this basket|

*REST: Sample Request*

```
/global/api2/basket.cfc?method=remove&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&basket_id=7859437598-2345-2345&asset_id=108
```

*Sample Output*

```
{["responsecode":"0","message":"File have been removed from this basket"]}
```	
___

**Download basket**

> **Downloading basket** : *Please note, that downloading the basket has **two** parts!* 

> *One is the method downloadBasket(). This method initiates the collection of all files in the basket and then creates a ZIP file for downloading. The returning value (the ZIP file) of downloadBasket() can then be used in the *second" method, checkForBasket(), to check if the file is ready to download. Files are made available in a special directory called /tmp on your server. The full URL to the basket file depends on your installation but usually it is something like, e.g. (domain)/global/tmp/ZIPFILE or (domain)/razuna/global/tmp/ZIPFILE.*

> *These methods will help you to create your own feedback to the client. This can either be a loading bar, a message or send them an email after the basket is ready.*

___

**Method to initiate download**

|Method name|Returns|
|-----------|-------|
|downloadBasket|String|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|basket_id|Basket ID of the comment|String|yes|7859437598-2345-2345|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|responsecode|A response number|0 = success|
|message|Name of ZIP file|basket-89749837.zip|

*REST: Sample Request*

```
/global/api2/basket.cfc?method=downloadBasket&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&basket_id=7859437598-2345-2345
```

*Sample Output*

```
{["responsecode":"0","message":"basket-89749837.zip"]}
```
___

**Method to check for basket availability**

|Method name|Returns|
|-----------|-------|
|checkForBasket|String|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|zip_file|Name of ZIP file|String|yes|basket-89749837.zip|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|responsecode|A response number|0 = success|
|message|File availablity|true = available ; false = unavailable|

*REST: Sample Request*

```
/global/api2/basket.cfc?method=checkForBasket&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&zip_file=basket-89749837.zip
```

*Sample Output*

```
{["responsecode":"0","message":"true"]}
```
