# API Guide

On this page

   * Upgrading from API1 to API2
   * API Key
   * Available API Calls
   * API Requests

 Important Information about this version : 

`The API version 2 is available as of Razuna 1.5 and on the hosted platform as of March 26th 2012 !!!` 

 **API usage on the Hosted Platform**
`If you use the API against the hosted Razuna platform, please make sure that your data plan is within your accounts bandwidth and storage quota. If your bandwidth or storage is exceeded any API operation will fail to work!`
___

**Welcome to the Razuna API (version 2)**

The Razuna API allows you to connect your application to your assets in Razuna. You can upload, edit and remove assets, add and update users, create folders and much more trough the API methods. The Razuna API is based on REST and uses JSON, JSONP (JSON with Padding) and XML (WDDX) as data structure. You as the developer can manipulate in which format the data structure should be. Especially, the JSONP support makes cross-domain scripting in Javascript with Razuna a piece of cake. 

___

**Upgrading from API1 to API2**

If you are coming from version 1 of the API, then there are a couple of changes, which are:

* The API works now with an API KEY (each user has an API key).
* The API is now based on REST calls only (no more SOAP).
* As data structure we return now JSON (default), JSONP or XML (WDDX).
* You can directly influence what data structure you want to return.
* Most methods return complete record sets.
* You can now use JSONP to create a Javascript based application, e.g. JQuery method like $.getJSON().
* The API base URL is serverip/global/api2 !
* Please read the description of each method carefully, since we've made a lot of changes to the parameters.
___

**API Key**

In order to access the API you need to pass the API key with each method. The API key of each user can be found within the Razuna User dialog which will contain an 'API Key' tab displaying the API key. 

   * DAM Administrators can get to the user dialogs under the 'Users' tab in 'Administration' by clicking on a username.
   * Users can get to their user dialog by clicking on the menu next to their name on the top right corner when they are logged in and then selecting 'My Info'. 

REST

* Razuna Razuna Hosted Platform :

| The URL for Razuna API on the Razuna Hosted Platform is: api.razuna.com.|
|-------------------------------------------------------------------------|

API Method Request Format: API methods are encapsulated by web pages within the API web site. To call a method, make a POST or GET request to the web page corresponding to the method you want to execute.

Sample URL:

```
http://api.razuna.com/global/api2/assets.cfc?method=getasset&api_key=CA1EBCFD45084E3991EA569DB10A29AA&assetid=108
```

When an API method is called, a response is returned to the caller in JSON (default), JSONP or XML (WDDX) format (WDDX (Web Distributed Data eXchange) is a established standard. More information is available over at WDDX at Wikipedia). By default, the API will return JSON. If you want to receive JSONP or XML you have to append "&__BDRETURNFORMAT=wddx" or "&__BDRETURNFORMAT=jsonp" to your call. NOTE: In order for JSONP to work you will need to append additionally "callback=?"!

Example JSON output (if a record set is being returned):

```
{"columns":["ID"],"data":["108"]}
```

By default the API will return a ROW based JSON. If you want to use a COLUMNS you simply need to append the parameter "&__BDQUERYFORMAT=column" and the API will output:

```
{"columns":["ID"],"data"{"id":["108"]}}
```

Now, in order to get JSONP (JSON with Padding) you would issue the following call within your Javascript (we use JQuery here) to the API:

```
$.getJSON(
 "http://api.razuna.com/global/api2/assets.cfc?method=getasset&api_key=CA1EBCFD45084E3991EA569DB10A29AA&assetid=108&__BDRETURNFORMAT=jsonp&callback=?",
  function(json){
    // do something with the 'json' object
  }
);
```

The output for the above will be:

```
?({"columns":["ID"],"data":["108"]})
```
___

**Available API Calls**

The following API sections are available:

   * Upload API2
   * Search API2
   * Asset API2
   * Folder API2
   * Collection API2
   * Label API2
   * Custom Fields API2
   * User API2
   * Group API2
   * Hosts API2
   * Comment API2
   * Basket API2
___
###Upload API2

With the below description you can upload assets to your Razuna installation remotely.

*Uploading assets remotely*

Uploading assets within your application has to actually happen with posting the asset to the Razuna web service. The http protocol allows a multipart/form-data POST (RFC 1867) to upload files. You have to pass the required parameters in the form data. These must precede any multipart form data which contains file content. This allows us to verify security before attempting to accept the upload, if this is not done you will receive an error.

The maximum content size is limited to the maximum content-length of a HTTP request. If you exceed the maximum value you get a 10001 error.


Since this is a post directly into Razuna, the URL for this API call differs from the rest. Thus your endpoint will be the index file of your tenant/host. Example: [http://localhost:8080/razuna/raz1/dam/index.cfm](http://localhost:8080/razuna/raz1/dam/index.cfm.) (Obviously you'll need to adjust the URL for your installation).

If you develop on our Razuna Shared Platform your endpoint is your subdomain, e.g [http://demo.razuna.com/index.cfm](http://demo.razuna.com/index.cfm)

 * Input Parameter

|Parameter|Description|Type|Required|Sample Input|Version|
|---------|-----------|----|--------|------------|-------|
|api_key|A valid api_key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943||
|debug|If you turn debug on you will receive an email with the values you are passing to the API|boolean|no|0 = false (default) 1 = true||
|destfolderid|The folder you want to store the asset in|String|yes|1||
|emailto|Enter your eMail address in order to receive the debug email|string|no|valid email||
|fa|required parameter is "c.apiupload"|String|yes|c.apiupload||
|filedata|The name of the file field (filedata)|File field|yes|This field has to be named "filedata" !||
|meta_lang_id_r|Set the language you want to write the metadata for. Mandatory if you want to write metadata!|numeric|no|1 = English   2 = German   etc.|Razuna 1.4.5   |
|metadata|Set this to 1 to add metadata during upload. Please note important information below!|boolean|no|0 = false (default)  1 = true  |Razuna 1.4.5|
|redirectto|A full URL where to redirect the output of the upload|string|no|[http://razuna.domain.com/index.html](http://razuna.domain.com/index.html) ; You will get a response with "responsecode=(0)&message=(status message)&assetid=(asset id)"|Razuna 1.4.4 adds the assetid return parameter|
|redirecttoparams|Additional parameters you would like to pass to the "redirectto" string above|string|no|param1=value1&param2=value2 ; These parameters will get added to the redirectto string "responsecode=(0)&message=(status message)&assetid=(asset id)&param1=value1&param2=value2" ; Note: Don't add the first "&" as the system will do this automatically|Razuna 1.4.4|
|skip_event|The event name you want to skip (only in combination with the workflow plugin)|String|no|on_pre_process = Pre-Process on_file_add = Add file(s) on_file_edit = Edit file(s) on_file_move = Move file(s) on_file_remove = Delete file(s) on_folder_add = Add folder on_folder_edit = Edit folder on_folder_move = Move folder on_folder_remove = Delete folder  .You can skip many events by separating each event with a comma, e.g. "on_pre_process,on_file_add"|Razuna 1.6|
|upl_template|ID of the upload template to execute|String|no|54592180064BC7466F4B2F943|Razuna 1.6|
|zip_extract|To extract a ZIP archive after uploading or not|boolean|no|0 = false 1 = true (default)||




How to add metadata to your asset during upload

As of Razuna 1.4.5 you can populate the metadata fields during the upload. For this to work you need to add the field "metadata" to your post with the value "1". Furthermore, you need to prefix each metadata field with "meta_". A list of the correct and available metadata fields is available here.
```
Example: Populate the description, keywords and the location metadata:
meta_img_description = "My description"
meta_img_keywords = "razuna, image, eyes"
meta_location = "New York"
meta_lang_id_r = 1
```
Important
You DO NOT need to pass a JSON structure. Razuna reads your form fields automatically!
___
*Output Value*

The below will be returned to you in XML format.

|Name|Description|Sample Output|Note|
|----|-----------|-------------|----|
|Response|A result code with the status of the login. If the result is 0 the method was successful.|0||
|message|Returning message|success||
|assetid|The ID of the asset in Razuna|2EC82EE9EF03499FBCA4247D99F026B1|Version 1.4.4|
|filetype|The file type (img = image, vid = video, aud = audio, doc = document, other = other format|img|Version 1.4.4|
|comingfrom|The HTTP referrer of the request|http://myuploadscript|Version 1.6|
|renamefilebody	|Requests coming back when using the workflow pre-process rename action||Version 1.6 in combination of the Workflow plugin|

Sample HTTP Form 

``` 
<form action="http://demo.razuna.com/index.cfm" name="up" method="post" enctype="multipart/form-data">
<input type="hidden" name="fa" value="c.apiupload">
<input type="hidden" name="api_key" value="54592180-7060-4D4B-BC74-2566F4B2F943">
<input type="hidden" name="destfolderid" value="1">
 
<input type="file" name="filedata">
 
<input type="submit" value="send it">
</form> 
```
Sample CURL command

```
curl -X POST -H "Expect: " -F fa=c.apiupload -F destfolderid=C78950B868CE48168E6DD73CFC8B6519 -F filedata=@myimage.jpg -F api_key=545921807064D4BBC742566F4B2F943 http://demo.razuna.com/index.cfm
```

* Demo Upload Templates :

We have made two examples of uploading assets to Razuna within the API2/demo folder. One example is a simple form post and the other a integration with the popular SWFUpload uploader. You will need to run these two examples from within Razuna in order to work, since they work with Razuna only. 

Flash or Flex :

If you are using a Flash, Flex or AIR application to upload assets to Razuna you will need to use the URL with parameters since Flash only send the filedata id in the post. So you would use the URL of the form action like: [http://demo.razuna.com/index.cfm?fa=c.apiupload&sessiontoken=54592180-7060-4D4B-BC74-2566F4B2F943&destfolderid=1&zip_extract=1](http://demo.razuna.com/index.cfm?fa=c.apiupload&sessiontoken=54592180-7060-4D4B-BC74-2566F4B2F943&destfolderid=1&zip_extract=1)

___

###Search API2

*Search and finding assets*

Method

|Method Name|Returns|	
|-----------|-------|
|searchassets|Record set|

Input Parameter

|Parameter|Description|Type|Required|Sample Input|(Dates are in European format)|
|---------|-----------|----|--------|------------|------------------------------|
|api_key|A valid api key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943||
|searchfor|The search entry. Same search syntax as in Search and Find Assets applies.|String|yes|Your search term.You can use the same search syntax as within Razuna.Please see Search and Find Assets ||
|show|What kind of assets to show|String|no|all = All assets (default) img = Images onlyvid = Videos only doc = Documents only aud = Audios only ||
|doctype|Filters the doc type. Only applies if "show" is set to "doc"!|String|no|empty = All doc types (default) pdf = PDF xls = Excel doc = Word other = All other types||
|datecreate|Search for files creation date|String|no|Example: 2012-11-08 or 20121108|Razuna 1.6 Hosted Edition 11.11.2012 |
|datechange|Search for files modification/changed date|String|no|Example: 2012-11-08 or 20121108|Razuna 1.6 Hosted Edition 11.11.2012|
|datecreaterange|Search for files created within the given date range|String|no|Example: 20150601 TO 20150701|Razuna 1.7.5 Hosted Edition 19.07.2015|
|datechangerange|Search for files modified within the given date range|String|no|Example: 20150601 TO 20150701|Razuna 1.7.5 Hosted Edition 19.07.2015|
|folderid|When a folderid is being used, the search will only include results within this folder.|String|no|489427894|Razuna 1.6 Hosted Edition 25.11.2012 |
|sortby|Option to sort results (see sample)|String|no|Sort is according to the following values: name = filename (default) ; sizedesc = size descending ; sizeasc = size ascending ; dateadd = create date descending ; datechanged = change date descending |Razuna 1.6 Hosted Edition 06.03.2013 |
|available|Show all files that are fully processed and available|String|no|	1 (default) = is processed  0 = not processed	| Razuna 1.6 Hosted Edition 01.09.2013 |
|startrow|The row to start at. Will return results from this row on. Example: In order to get the next 25 results you would start from row 26!|Number|no|1 = default|Razuna 1.7.5 Hosted Edition 15.04.2015|
|maxrows|Maximum of records to return in the search.|Number|no|25 = default|Razuna 1.7.5 Hosted Edition 15.04.2015| 
|showrenditions|Option to include renditions in the returning data load|boolean|no|true (default) ; false|Razuna 1.7.5 Hosted Edition 06.05.2015|
|dbdirect|Set this to "true" to query the database directly.This also supports the "search for" parameter. But it will only search in the filename. Additionally, it supports the LIKE search. To do so you need to use "%". NOTE: Doesn't work with "show" and "doctype" parameters.|String|no|false (default) ; true|Razuna 1.6 Hosted Edition 01.09.2013|
|datecreateparam (can only be used in combination with dbdirect!)|SQL Parameter to use for getting records|String|no|>, <, =>, =<, between, etc.|Razuna 1.6 Hosted Edition 13.12.2012|
|datecreatestart (can only be used in combination with dbdirect!)|The start date and time|String|no|Format has to be "yyyy-mm-dd 00:00:00". Example: 2012-12-11 17:00:00|Razuna 1.6 Hosted Edition 13.12.2012|
|datecreatestop (can only be used in combination with dbdirect!)|The end date and time (used if you want to search with BETWEEN|String|no|Format has to be "yyyy-mm-dd 00:00:00". Example: 2012-12-11 17:00:00|Razuna 1.6 Hosted Edition 13.12.2012|
|datechangeparam (can only be used in combination with dbdirect!)|SQL Parameter to use for getting records|String|no|>, <, =>, =<, between, etc.|Razuna 1.6 Hosted Edition 13.12.2012|
|datechangestart (can only be used in combination with dbdirect!)|The start date and time|String|no|Format has to be "yyyy-mm-dd 00:00:00". Example: 2012-12-11 17:00:00|Razuna 1.6 Hosted Edition 13.12.2012|
|datechangestop (can only be used in combination with dbdirect!)|The end date and time (used if you want to search with BETWEEN)|String|no|Format has to be "yyyy-mm-dd 00:00:00". Example: 2012-12-11 17:00:00|Razuna 1.6 Hosted Edition 13.12.2012|

> **Field search:**

> As mentioned the search via API supports the same syntax as the search within Razuna. In other words you can search generally as just providing a search term (example: "audrey hepurn") or provide a more field like search. The field search especially allows you to search for words in "keywords, "description", "labels", etc. Example: labels:myLabel or keywords:audrey.
	
*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|Response|A result code with the status of the login. If the result is 0 the method was successful.|0|
|totalassetscount|How many assets are in this folder|8|	
|calledwith|The search term you called with method with|Audrey Hepurn|
|list of fields|the list of fields of each asset|see sample output|

> Updates

> As of Razuna 1.6 (hosted edition since 11.11.2012) the search additionally returns the create and change dates of each record.

> As of Razuna 1.6 (hosted edition since 16.12.2012) the search also returns the collection id(s) the file might be in in the column "colid"

`Remember to always encode your URL parameters!`

**REST: Sample request**

```
/global/api2/search.cfc?method=searchassets&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&searchfor=batman*
```

**REST: Sample request with multiple search criteria (showing only images and renditions)**

```
/global/api2/search.cfc?method=searchassets&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&searchfor=batman*&show=img&showrenditions=true
```

**REST: Sample request for getting files within a given date range**

```
/global/api2/search.cfc?method=searchassets&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&searchfor=batman&datecreaterange=20150601 TO 20150701
```

**REST: Sample request search within a date range and the dbdirect method**

```
/global/api2/search.cfc?method=searchassets&api_key=54592180-7060-4D4B-BC74-2566F4B2F943
&searchfor=batman*&dbdirect=true&datecreatestart=2012-12-11 17:00:00&datecreatestop=2012-12-12 17:00:00&datecreateparam=between
```

**Sample Output**

```
{"columns":["id","filename","folder_id","extension","video_image","filename_org","kind","extension_thumb","path_to_asset","cloud_url","cloud_url_org","size","width","height","description","keywords","rowtotal","local_url_org","local_url_thumb","responsecode","totalassetscount","calledwith"],"data":[["5DBE0927C6AA4212B0001930C0F7D7A5","01.14.12
 Affliction LA Lookbook
36475-Edit.tif","4564659C48B348C7B5DAF95AE6C3854E","jpg","dummy","2.jpg","img","jpg","4564659C48B348C7B5DAF95AE6C3854E/img/5DBE0927C6AA4212B0001930C0F7D7A5","","","65493",550,549,"","This
 is a
demo",2,"http://localhost:8080//assets/1/4564659C48B348C7B5DAF95AE6C3854E/img/5DBE0927C6AA4212B0001930C0F7D7A5/2.jpg","http://localhost:8080//assets/1/4564659C48B348C7B5DAF95AE6C3854E/img/5DBE0927C6AA4212B0001930C0F7D7A5/thumb_5DBE0927C6AA4212B0001930C0F7D7A5.jpg",0,2,"audrey"]]} 
```

> **Output Format :**

> Remember you can adjust the output dynamically. The API returns JSON by default. For record sets it defaults to a ROW based set, if you need COLUMNS simply append "&__BDQUERYFORMAT=column" to your call. In case, you need JSONP you want to append "&__BDRETURNFORMAT=jsonp&callback=?". In order to retrieve XML (WDDX) you simply need to append "&__BDRETURNFORMAT=wddx".

**Search for Labels**

Since Razuna 1.5 there is also the option to search for labels. Since the search API depends on the search within Razuna you can also leverage the label search within the API. In order to do so, you simply do a field search as in:

```
labels:(Animals)
```

In this example; "Labels" is the field and "Animals" is the label. Simply add this to the searchtext as in any other search and it would looks like this:

```
/global/api2/search.cfc?method=searchassets&api_key=54592180-7060-4D4B-BC74-2566F4B2F943
&searchfor=labels:(Animals)
```

Remember to escape any paramater so the searchtext would actually be encoded and be "&searchtext=labels%3A(Animals)".

As in any other search you might want to combine many labels in your search. As an example, I would have an asset taged with "Animals" and "Animals/Big Animals". In this case, we would "AND" them all together and combine them into a field search as in:

```
/global/api2/search.cfc?method=searchassets&api_key=54592180-7060-4D4B-BC74-2566F4B2F943
&searchfor=labels:(Animals),(Animals+big+animals)
```

Again, you need to encode the URL as in this example it would be "&searchtext=labels%3A(Animals)%2C(Animals+big+animals)". You only need to URL encode characters outside the "()"!

**Search for Custom Fields**

Just as with Labels you have the option to integrate custom fields in your search since Razuna 1.5.

As custom fields can be dynamically created within Razuna or the API, you will need to know the custom field ID to search against. (You can grab the ID within Razuna or by [querying the Custom Fields API](http://wiki.razuna.com/display/ecp/Custom+Fields+API2)). Once you now the field ID you add the ID and your value together and execute the search. As in:

```
customfieldvalue:(+255F307E-AE5A-4E66-AD2F6BBE81D0541C +:audrey)
```

In this example, we assume that my custom field ID is "255F307E-AE5A-4E66-AD2F6BBE81D0541C" and the value I'm looking for is "audrey". Again, just like with any other search, you need to add this to your API call as in:

```
/global/api2/search.cfc?method=searchassets&api_key=54592180-7060-4D4B-BC74-2566F4B2F943
&searchfor=customfieldvalue:(+255F307E-AE5A-4E66-AD2F6BBE81D0541C +audrey)
```

NOTE: You NEED to combine them with () in order for the search to work properly. In order to search for many custom field value you can combine the search like this:

```
/global/api2/search.cfc?method=searchassets&api_key=54592180-7060-4D4B-BC74-2566F4B2F943
&searchfor=customfieldvalue:(+255F307E-AE5A-4E66-AD2F6BBE81D0541C +audrey) AND customfieldvalue:(+237503B5-BB08-4658-8E4EFC2759847F07 +T)
```

As of Razuna 1.7.5 the select multiple field is available. In order to search for multiple values in in a custom field you simply "+" the values in your API call:

```
/global/api2/search.cfc?method=searchassets&api_key=54592180-7060-4D4B-BC74-2566F4B2F943
&searchfor=customfieldvalue:(+255F307E-AE5A-4E66-AD2F6BBE81D0541C +audrey +female +beauty)
```

> Remember to always encode your URL parameters! Example: customfieldvalue%253A(%252BF3013F39-D493-4D06-A44A04C5145D3AC7%2520%252B048001213364)

As you can see, the search allows for some very powerful ways to query your storage store within Razuna and only retrieve the assets you need within your application. Now, with the power of the above examples we are sure you can come up with some very useful methods to add Razuna to your existing application stack.

___

**Indexing/rebuilding the search index**

> **Availability**

> This API method is available since the 1.6 release (hosted platform as of September 2013)

The below API method gives you the option to trigger the indexing of all files not indexed yet, triggering indexing of individual files (re-index) or trigger a full re-build (indexing of all files in your library).

*Method*

|Method Name|Returns|
|-----------|-------|
|searchIndex|Status|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|assetid|The id of the asset or a list of id's (delimited with a ",")|String|yes|Possible values are: assetid = single assetid or list of assetids all = rebuild search index|

*Output Value*

|Parameter|Description|Type|Required|Sample Output|
|---------|-----------|----|--------|-------------|
|Response|A result code with the status. If the result is 0 the method was successful.|0|
|message|Message of the result|see sample output|

**REST: Sample Request**

```
/global/api2/search.cfc?method=searchIndex&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&assetid=108,109,110
```
Sample Output

```
{["responsecode":"0","message":"Indexing successfully triggered"]}
```

___

###Asset API2

**Get asset information**

*Method*

|Method Name|Returns|
|-----------|-------|
|getasset|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|assetid|The id of the asset or a list of id's (delimited with a ",")|String|yes|108 or 108,109,etc.|
|assettype|Type of asset|String|yes|doc = Documents img = Images vid = Videos aud = Audios|

*Output Value*

|Parameter|Description|Sample Input|
|---------|-----------|------------|
|Response|A result code with the status. If the result is 0 the method was successful.|0|
|totalassetcount|Numbers of records found|8|
|calledwith|The folderid you passed to this method|108|
|assets|For each asset an asset node is returned with information of the asset|see sample output|

> Since Razuna 1.4.6 the return also contains the "RAW" metadata fields of each asset in the node <metadata>. If you want to retrieve single metadata field you can use the dedicated [getmetadata()](http://wiki.razuna.com/display/ecp/Asset+API2#AssetAPI2-getmeta) method, also.

> As of Razuna 1.5.5 (hosted edition since 16.12.2012) the search also returns the collection id(s) the file might be in in the column "colid".	

*REST: Sample Request*

```
/global/api2/asset.cfc?method=getasset&api_key=54592180-7060-4D4B-BC74-2566F4B2F943
&assetid=2424HJSFSD1234&assettype=img
```

*Sample Output*

```
{"columns":["id","filename","folder_id","extension","filename_org","extension_thumb","size","width","height","description","keywords","path_to_asset","cloud_url","cloud_url_org","metadata","hassubassets",
"local_url_org", "local_url_thumb","responsecode","totalassetscount","calledwith"],"data":[["5DBE0927C6AA4212B0001930C0F7D7A5","01.14.12 Affliction LA Lookbook 36475-Edit.tif","4564659C48B348C7B5DAF95AE6C3854E","jpg","2.jpg","jpg","65493",550,549,"","This is a demo","4564659C48B348C7B5DAF95AE6C3854E/img/5DBE0927C6AA4212B0001930C0F7D7A5","","","metadata here","true","http://localhost:8080//assets/1/4564659C48B348C7B5DAF95AE6C3854E/img/5DBE0927C6AA4212B0001930C0F7D7A5/2.jpg","http://localhost:8080//assets/1/4564659C48B348C7B5DAF95AE6C3854E/img/5DBE0927C6AA4212B0001930C0F7D7A5/thumb_5DBE0927C6AA4212B0001930C0F7D7A5.jpg","0",1,"5DBE0927C6AA4212B0001930C0F7D7A5"]]}
```

> *Output format*

> Remember you can adjust the output dynamically. The API returns JSON by default. For record sets it defaults to a ROW based set, if you need COLUMNS simply append "&__BDQUERYFORMAT=column" to your call. In case, you need JSONP you want to append "&__BDRETURNFORMAT=jsonp&callback=?". In order to retrieve XML (WDDX) you simply need to append "&__BDRETURNFORMAT=wddx".

___

**Get rendition of asset**

*Method*

|Method name|Returns|
|-----------|-------|
|getrenditions|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|Version|
|---------|-----------|----|--------|------------|-------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943||
|assetid|The id of the asset or a list of id's (delimited with a ",")|String|yes|108 or 108,109,etc.||
|assettype|Type of asset|String|yes|aud = Audios img = Images vid = Videos doc = Documents* *There are no "renditions" for documents. If you have added "additional renditions" then these will be listed!|deprecated as of 1.6.2|

*Output Value*

|Name|Description|Sample Input|
|---------|-----------|------------|
|fields with values|fields with values|see sample output|

*REST: Sample Request*

```
/global/api2/asset.cfc?method=getrenditions&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&assetid=108&assettype=img
```

*Sample Output*

```
{"COLUMNS":["type","id","width","height","path_to_asset","cloud_url_org","filename_org","extension","size","local_url_org","colorspace","xdpi","ydpi","unit","md5hash","parentid"],"DATA":[["rendition","46AAC84C9CC545F9ADCE9C9F3A640C6B",1936,1446,"CA3FE469A0B24E39B38620D104A9C0E8/img/46AAC84C9CC545F9ADCE9C9F3A640C6B","","IMG_0025_46AAC84C9CC545F9ADCE9C9F3A640C6B.png","png","5299612","http://razuna.org/assets/1/CA3FE469A0B24E39B38620D104A9C0E8/img/46AAC84C9CC545F9ADCE9C9F3A640C6B/IMG_0025_46AAC84C9CC545F9ADCE9C9F3A640C6B.png","sRGB","","","inches","3111ED783CB4207EA40B1F3AF225D6EC","42F8CDE558D5490A9ECA7C606B7B1ED0"],["rendition","D4EB0A38D2C04165A914FCE803C8A28C",1936,1446,"CA3FE469A0B24E39B38620D104A9C0E8/img/D4EB0A38D2C04165A914FCE803C8A28C","","IMG_0025_D4EB0A38D2C04165A914FCE803C8A28C.tif","tif","1592476","http://razuna.org/assets/1/CA3FE469A0B24E39B38620D104A9C0E8/img/D4EB0A38D2C04165A914FCE803C8A28C/IMG_0025_D4EB0A38D2C04165A914FCE803C8A28C.tif","sRGB","","","inches","CE68ADF6CF8659AAD6D2173F15C5DC0C","42F8CDE558D5490A9ECA7C606B7B1ED0"],["org","42F8CDE558D5490A9ECA7C606B7B1ED0",1936,2592,"CA3FE469A0B24E39B38620D104A9C0E8/img/42F8CDE558D5490A9ECA7C606B7B1ED0","","IMG_0025.jpg","jpg","2567742","http://razuna.org/assets/1/CA3FE469A0B24E39B38620D104A9C0E8/img/42F8CDE558D5490A9ECA7C606B7B1ED0/IMG_0025.jpg","sRGB","72","72","inches","08FD97C82969B24C1281A86B1E93B319",""],["thumb","42F8CDE558D5490A9ECA7C606B7B1ED0",400,299,"CA3FE469A0B24E39B38620D104A9C0E8/img/42F8CDE558D5490A9ECA7C606B7B1ED0","","IMG_0025.jpg","jpg","2567742","http://razuna.org/assets/1/CA3FE469A0B24E39B38620D104A9C0E8/img/42F8CDE558D5490A9ECA7C606B7B1ED0/thumb_42F8CDE558D5490A9ECA7C606B7B1ED0.jpg","sRGB","72","72","inches","08FD97C82969B24C1281A86B1E93B319",""],["rendition","B63F7B65DEF549B6813AE1E3D76352E2",0,0,"","http://razuna.org/images/test.png","test","img","0","http://razuna.org/images/test.png","","","","","","42F8CDE558D5490A9ECA7C606B7B1ED0"]]}
```



*Output format*

Remember you can adjust the output dynamically. The API returns JSON by default. For record sets it defaults to a ROW based set, if you need COLUMNS simply append "&__BDQUERYFORMAT=column" to your call. In case, you need JSONP you want to append "&__BDRETURNFORMAT=jsonp&callback=?". In order to retrieve XML (WDDX) you simply need to append "&__BDRETURNFORMAT=wddx".

___

**Get Metadata of asset**

> The getasset() method already returns the description and the keyword value for each asset, thus this method only returns the associated XMP metadata values! 

> Only PDF documents and images contain additional metadata. Obviously this method only works for "doc" and "img"!

*Method*	

|Method name|Returns|
|-----------|-------|
|getmetadata|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|assetid|The id of the asset or a list of id's (delimited with a ",")|String|yes|108 or 108,109,etc.|
|assettype|Type of asset|String|yes|doc = Documents (PDF) img = Images|
|assetmetadata|Name of metadata field to query|String|yes|headline,city,rights See the metadata field list below!|

**Metadata parameters**

*Documents*

|Metadata fields|
|---------------|
|author|
|rights|
|authorsposition|
|captionwriter|
|webstatement|
|rightsmarked|

*Images*

|Metadata fields|
|---------------|
|asset_type|
|subjectcode|
|creator|
|title|
|authorsposition|
|captionwriter|
|ciadrextadr|
|category|
|supplementalcategories|
|urgency|
|description|
|ciadrcity|
|ciadrctry|
|location|
|ciadrpcode|
|ciemailwork|
|ciurlwork|
|citelwork|
|intellectualgenre|
|instructions|
|source|
|usageterms|
|copyrightstatus|
|transmissionreference|
|webstatement|
|headline|
|datecreated|
|city|
|ciadrregion|
|country|
|countrycode|
|scene|
|state|
|credit|
|rights|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|metadata|Your passed fields with values|"values"|

*REST: Sample Request*

```
/global/api2/asset.cfc?method=getmetadata&api_key=54592180-7060-4D4B-BC74-2566F4B2F943
&assetid=108&assettype=img&assetmetadata=headline,city,rights
```

*Sample Output*

```
{"columns":["headline","city","rights"],"data":[["Some people standing","New York","Copyright"]]} 
```

> Output Format :

> Remember you can adjust the output dynamically. The API returns JSON by default. For record sets it defaults to a ROW based set, if you need COLUMNS simply append "&__BDQUERYFORMAT=column" to your call. In case, you need JSONP you want to append "&__BDRETURNFORMAT=jsonp&callback=?". In order to retrieve XML (WDDX) you simply need to append "&__BDRETURNFORMAT=wddx".

___

**Modify metadata of asset**

*Method*

|Method name|Returns|
|-----------|-------|
|setmetadata|String|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|assetid|The id of the asset or a list of id's (delimited with a ",")|String|yes|108 or a list like 108,109,etc.|
|assettype|Type of asset|String|yes|doc = Documents img = Images vid = Videos aud = Audios|
|assetmetadata||String|yes|JSON structure of metadata See the metadata field list below|

*Metadata parameters*

You can pass all or any of the metadata fields in the assetmetadata field as a JSON structure. A example of passing the metadata for images would be (you need to serialize your array in order to pass it in a URL):

```
[["lang_id_r","1"],["file_name","new file name"],["img_keywords","Razuna, Wordpress, Tomcat"],["img_description","Razuna Enterprise"],["creator","Nitai Aventaggiato"],["title","CTO"]]
```

> Mandatory field : The only mandatory field you need to include is the "lang_id_r" one.

*Videos*

|Metadata fields||
|---------------|----------------|
|vid_keywords||
|vid_description||
|lang_id_r||
|file_name|Razuna 1.5.5 (hosted since 11.11.2012)|

*Documents*

|Metadata fields||
|---------------|----------------|
|file_keywords||
|filedesc||
|lang_id_r||
|file_name|Razuna 1.5.5 (hosted since 11.11.2012)|

*Audios*

|Metadata fields||
|---------------|----------------|
|aud_keywords||
|aud_description||
|lang_id_r||
|file_name|Razuna 1.5.5 (hosted since 11.11.2012)|

*Images*

|Metadata fields||
|---------------|----------------|
|img_keywords||
|img_description||
|lang_id_r||
|file_name|Razuna 1.5.5 (hosted since 11.11.2012)|

For images you additionally have the option to define the XMP metadata values. The following fields can be used:

|Metadata fields|
|---------------|
|asset_type|
|subjectcode|
|creator|
|title|
|authorsposition|
|captionwriter|
|ciadrextadr|
|category|
|supplementalcategories|
|urgency|
|description|
|ciadrcity|
|ciadrctry|
|location|
|ciadrpcode|
|ciemailwork|
|ciurlwork|
|citelwork|
|intellectualgenre|
|instructions|
|source|
|usageterms|
|copyrightstatus|
|transmissionreference|
|webstatement|
|headline|
|datecreated|
|city|
|ciadrregion|
|country|
|countrycode|
|scene|
|state|
|credit|
|rights|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|Response|A result code with the status. If the result is 0 the method was successful.|0|
|Message|Status Message|Metadata successfully stored|

*REST: Sample Request*

```
/global/api2/asset.cfc?method=setmetadata&api_key=54592180-7060-4D4B-BC74-2566F4B2F943
&assetid=108&assettype=img&assetmetadata=[["lang_id_r","1"],["img_keywords","Razuna, Wordpress, Tomcat"],["img_description","Razuna Enterprise"],["creator","Nitai Aventaggiato"],["title","CTO"]]
```

*Sample Output*

```
{["responsecode":"0","message":"Metadata successfully stored"]}
```

___

**Remove Asset**

This method can also be used to remove renditions. Simply pass in the id of the rendition in the assetid parameter.

*Method*


|Method name|Returns|
|-----------|-------|
|remove|String|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|assetid|The id of the asset or a list of id's (delimited with a ",")|String|yes|108 or a list like 108,109,etc.|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|Response|A result code with the status. If the result is 0 the method was successful.|0|
|message|Message of the result|see sample output|

REST: Sample Request

```
/global/api2/asset.cfc?method=remove&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&assetid=108,109,110
```

Sample Output

```
{["responsecode":"0","message":"Asset(s) have been removed successfully"]}
```

___

**Move Asset(s)**

> Availability : The "move" method is available as of Razuna 1.5.5 and on the hosted platform as of February 13th 2013.

*Method*

|Method name|Returns|
|-----------|-------|
|move|String|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|assetid|The id of the asset or a list of id's (delimited with a ",") or with the keyword "all"|String|yes|108 or a list like 108,109,etc. If you want to move ALL files in the folder you can use the keyword "all"! |
|source_folder|The folder ID where the current files are in|String|no ; required if you set assetid to "all" |2566F4B2F943|
|destination_folder|The folder ID the files should be moved to|String|yes|54592180|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|Response|A result code with the status. If the result is 0 the method was successful.|0|
|message|Message of the result|see sample output|

*REST: Sample Request*

```
/global/api2/asset.cfc?method=move&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&assetid=108,109,110&destination_folder=54592180
```

*Sample Output*

```
{["responsecode":"0","message":"Asset(s) have been moved successfully"]}
```
___

**Create renditions**

*Method*

|Method name|Returns|
|-----------|-------|
|createrenditions|String|

*Input Parameter*
	
|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|assetid|The id of the asset|String|yes|108 |
|assettype|Type of asset|String|yes|img = Images vid = Videos aud = Audios Note: There are no "renditions" for documents|
|convertdata|JSON structure of parameters for converting|String|yes|convertdata=[[["convert_to","jpg"],["convert_width_jpg","500"],["convert_height_jpg","374"],["convert_dpi_jpg",""],["convert_wm_jpg",""]]]|
|colorspace|Colorspace of asset : Images only|String	|no|Examples of Colorspace : HCL, YUV, Gray, Luv etc Reference for setting Colorspace values for an asset: [http://www.imagemagick.org/script/command-line-options.php#colorspace](http://www.imagemagick.org/script/command-line-options.php#colorspace) Note: If in the DAM administration under 'Settings' the 'Image Colorspace' is 'Set to RGB' then it will override this value. Set it back to default if you want this to take precedence.|

*Parameters for converting*

You can pass all or any of the metadata fields in the assetmetadata field as a JSON structure. A example of passing the metadata for images would be (you need to serialize your array in order to pass it in a URL):

```
convertdata=[[["convert_to","format"],["convert_width_format","value"],["convert_height_format","value"],["convert_dpi_format","value"],["convert_wm_format","value"]]]
```	

The following parameters are valid: (You need to replace the (format) with the format you want to convert to)!

|Parameter|Description|Type|Required|Application for|Comment|
|---------|-----------|----|--------|------------|----------|
|convert_to|Format to convert to|String|yes|Images, Videos, Audios|All formats are supported that you can find in the Razuna interface!|
|convert_width_(format)|Width|Number|yes|Images, Video|For no value, just leave empty|
|convert_height_(format)|Type Height|Number|yes|Images, Video|For no value, just leave empty|
|convert_dpi_(format)|DPI|Number|yes|Images|For no value, just leave empty|
|convert_wm_(format)|The ID of the Watermark template|String|yes|Images|For no value, just leave empty|
|convert_bitrate_(format)|Bitrate of Audio file|Numer|yes|Audios|All bitrates are supported as displayed in the Razuna interface. Note: For FLAC and WMV; Just pass an empty value!|

*Example: Converting to a JPG*

```
http://localhost:8080/razuna/global/api2/asset.cfc?method=createrenditions&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&assetid=E9A8DED50AAB47FDBA38D6866D1809C9&assettype=img&convertdata=[[["convert_to","jpg"],["convert_width_jpg","500"],["convert_height_jpg","374"],["convert_dpi_jpg",""],["convert_wm_jpg",""]]]
```
*Example: Converting with DPI only*

```
http://localhost:8080/razuna/global/api2/asset.cfc?method=createrenditions&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&assetid=E9A8DED50AAB47FDBA38D6866D1809C9&assettype=img&convertdata=[[["convert_to","jpg"],["convert_width_jpg",""],["convert_height_jpg",""],["convert_dpi_jpg","300"],["convert_wm_jpg",""]]]
```

*Example: Converting with a Watermark*

```
http://localhost:8080/razuna/global/api2/asset.cfc?method=createrenditions&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&assetid=E9A8DED50AAB47FDBA38D6866D1809C9&assettype=img&convertdata=[[["convert_to","jpg"],["convert_width_jpg","500"],["convert_height_jpg","374"],["convert_dpi_jpg",""],["convert_wm_jpg","11E3009FB2804C68851024C10E7EF908"]]]
```

*Example: Converting to many formats*

```
http://localhost:8080/razuna/global/api2/asset.cfc?method=createrenditions&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&assetid=E9A8DED50AAB47FDBA38D6866D1809C9&assettype=img&convertdata=

[[["convert_to","jpg"],["convert_width_jpg","400"],["convert_height_jpg","300"],["convert_dpi_jpg",""],["convert_wm_jpg",""]],
 
 
[["convert_to","png"],["convert_width_png","350"],["convert_height_png","262"],["convert_dpi_png",""],["convert_wm_png",""]],


[["convert_to","gif"],["convert_width_gif","200"],["convert_height_gif","150"],["convert_dpi_gif",""],["convert_wm_gif",""]],


[["convert_to","bmp"],["convert_width_bmp","230"],["convert_height_bmp","230"],["convert_dpi_bmp",""],["convert_wm_bmp",""]]]
```

*Example: Converting with Colorspace*

```
http://localhost:8080/razuna/global/api2/asset.cfc?method=createrenditions&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&assetid=E9A8DED50AAB47FDBA38D6866D1809C9&assettype=img&convertdata=[[["convert_to","jpg"],["convert_width_jpg","500"],["convert_height_jpg","374"],["convert_dpi_jpg",""],["convert_wm_jpg","11E3009FB2804C68851024C10E7EF908"]]]&colorspace=transparent
```

*Sample Output*

```
{["responsecode":"0","message":"Asset has been converted successfully"]}
```
___

**Regenerate asset metadata**

*Method*

|Method name|Returns|
|-----------|-------|
|regeneratemetadata|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|assetid|The id of the asset or a list of id's (delimited with a ",")|String|yes|108 or 108,109,etc.|
|assettype|Type of asset|String|yes|doc = Documents img = Images vid = Videos aud = Audios|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|Response|A result code with the status. If the result is 0 the method was successful.|0|
|Message|Success or error message if error occurred|Metadata successfully stored|

*REST: Sample Request*

```
/global/api2/asset.cfc?method=regeneratemetadata&api_key=1693DDE9404642499A677B76F4682558&assetid=FFBF081AF38C4F8F891BB453532CD08B,14497C7221A040BA92A1C1BA822369D7&assettype=img
```

*Sample Output*

```
{"responsecode":0,"message":"Metadata successfully stored"}
```

___

**Get PDF Images Information**

*Method*

|Method name|Returns|
|-----------|-------|
|getpdfimages|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|49286DAD4B464CFBB60B3742AF193758|
|assetid|The id of the asset. Must be a PDF document.|String|yes|EEE8CC192B264D65A85C08990E5E57A1|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|assetid|The original assetid passed|EEE8CC192B264D65A85C08990E5E57A1|
|name|PDF image name, corresponds to a page in the PDF|Happiness-1.jpg|
|local_directory|Directory on machine where images are stored|/Users/scott/razuna_tomcat_1_6_RC_2/tomcat/webapps/razuna/assets/1/0031D211A15B42598580B84B035EBA8C/doc/EEE8CC192B264D65A85C08990E5E57A1/razuna_pdf_images|	
|size|Size of image in bytes|81448|
|local_url_org|URL to access the image|http://localhost:8080/razuna/assets/1/0031D211A15B42598580B84B035EBA8C/doc/EEE8CC192B264D65A85C08990E5E57A1/razuna_pdf_images/Happiness-1.jpg|

*REST: Sample Request*

```
/global/api2/asset.cfc?method=getpdfimages&api_key=49286DAD4B464CFBB60B3742AF193758&assetid=EEE8CC192B264D65A85C08990E5E57A1
```

*Sample Output (No Errors)*

```
{"COLUMNS":["assetid","name","local_directory","size","local_url_org"],"DATA":[["EEE8CC192B264D65A85C08990E5E57A1","HappinesswithfinalimagesFINALF-0.jpg","/Users/bubbles/Downloads/razuna_tomcat_1_6_RC_2/tomcat/webapps/razuna/assets/1/0031D211A15B42598580B84B035EBA8C/doc/EEE8CC192B264D65A85C08990E5E57A1/razuna_pdf_images",81448,"http://localhost:8080/razuna/assets/1/0031D211A15B42598580B84B035EBA8C/doc/EEE8CC192B264D65A85C08990E5E57A1/razuna_pdf_images/HappinesswithfinalimagesFINALF-0.jpg"],["EEE8CC192B264D65A85C08990E5E57A1","HappinesswithfinalimagesFINALF-1.jpg","/Users/bubbles/Downloads/razuna_tomcat_1_6_RC_2/tomcat/webapps/razuna/assets/1/0031D211A15B42598580B84B035EBA8C/doc/EEE8CC192B264D65A85C08990E5E57A1/razuna_pdf_images",16282,"http://localhost:8080/razuna/assets/1/0031D211A15B42598580B84B035EBA8C/doc/EEE8CC192B264D65A85C08990E5E57A1/razuna_pdf_images/HappinesswithfinalimagesFINALF-1.jpg"]]}
```

*Sample Output (If Errors)*

```
{"COLUMNS":["responsecode","message"],"DATA":[["1","Asset with the given assetid could not be found. Please check assetid and try again."]]}

```
___

###Folder API2

**Get a list of folders**

This method will return a list of folders on ONE level. To iterate for subfolders you will need to call this method each time.
	
*Method*

|Method name|Returns|
|-----------|-------|
|getfolders|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid api key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|folderid|The ID of the folder you want to retrieve assets from.|Numeric|no|0 = all folders on the root level|
|collectionfolder|If this is a collection folder|String|no|true ; false|

*Output Value*

|Name|Description|Sample Output|Note|
|----|-----------|-------------|----|
|folder_id|ID of folder|2||
|folder_name|Name of folder|Demo Folder||
|folder_owner|ID of user that owns the folder|0CA09066-05AA-4B22-B33C1CC6EED10F3E||
|username|Name of user that owns the folder|John||
|hassubfolders|Folder contains sub-folder|true or false||
|folder_description|Folder description|Upload folder|Razuna 1.5.5 (hosted edition 12.11.2012)|
|totalassets|Total of all assets in this folder. Only populated if not a collection folder.|8|Razuna 1.3.5|
|totalimg|Total of all assets in this folder. Only populated if not a collection folder.|5|Razuna 1.3.5|
|totalvid|Total of all assets in this folder. Only populated if not a collection folder.|2|Razuna 1.3.5|
|totaldoc|Total of all assets in this folder. Only populated if not a collection folder.|1|Razuna 1.3.5|
|totalaud|Total of all assets in this folder. Only populated if not a collection folder.|3|Razuna 1.3.5|
|howmanycollections|Number of collections in collection folder. Only populated if this is a collection folder.|1||

*REST: Sample Request*

```
/global/api2/folder.cfc?method=getfolders&api_key=54592180-7060-4D4B-BC74-2566F4B2F943
```

*Sample Output*

```
{"columns":["folder_id","folder_name","folder_owner","username","hassubfolders","folder_description","totalassets","totalimg","totalvid","totaldoc","totalaud","howmanycollections"],"data":
[["E6EA9B014E6046EAA3F4390E3ED77791","Demo","1","admin","true","Contains images only",170,0,0,0,0,1]]}
```

> **Output format :** 
> *Remember you can adjust the output dynamically. The API returns JSON by default. For record sets it defaults to a ROW based set, if you need COLUMNS simply append "&__BDQUERYFORMAT=column" to your call. In case, you need JSONP you want to append "&__BDRETURNFORMAT=jsonp&callback=?". In order to retrieve XML (WDDX) you simply need to append "&__BDRETURNFORMAT=wddx".*
	
___

**Retrieving all assets in a folder**

*Method*

|Method name|Returns|
|-----------|-------|
|getassets|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api key|A valid api key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|folderid|The ID of the folder you want to retrieve assets from.|String|yes|1|
|showsubfolders|To include assets from subfolders as well.|String|no|true ; false (default)|
|show|What kind of assets to show|String|no|all = All assets (default) img = Images only vid = Videos only doc = Documents only aud = Audios only|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|totalassetscount|How many assets are in this folder|8|
|calledwith|The folderid you passed to this method|1|
|listassets|The body node of the returned list of assets||
|assets|For each asset an asset node is returned with information of the asset|see sample output|

> **Updates :**
> *As of Razuna 1.5.5 (hosted edition since 16.12.2012) the search also returns the collection id(s) the file might be in in the column "colid"*
	
*REST: Sample Request*

```
/global/api2/folder.cfc?method=getassets&api_key=54592180-7060-4D4B-BC74-2566F4B2F943
&folderid=1
```

*Sample Output*

```
{"columns":["id","filename","folder_id","extension","video_image","filename_org","kind","extension_thumb","size","width","height","description","keywords","path_to_asset","cloud_url","cloud_url_org","subassets","local_url_org","local_url_thumb","responsecode","totalassetscount","calledwith"],"data":[["5E2EB2A833C542748E314DF54AF169BD","Rodnse.jpg","33D207AF29D1447E931A8210982FC4A3","jpg","dummy","Rodnse.jpg","img","jpg","53134",412,569,"This
 is a demo","contains german u,another a in
here","33D207AF29D1447E931A8210982FC4A3/img/5E2EB2A833C542748E314DF54AF169BD","","","false","http://razunabd.local:8080//assets/1/33D207AF29D1447E931A8210982FC4A3/img/5E2EB2A833C542748E314DF54AF169BD/Rodnse.jpg","http://razunabd.local:8080//assets/1/33D207AF29D1447E931A8210982FC4A3/img/5E2EB2A833C542748E314DF54AF169BD/thumb_5E2EB2A833C542748E314DF54AF169BD.jpg","0",1,"33D207AF29D1447E931A8210982FC4A3"]]}

```
Error rendering macro 'excerpt-include' : null
___

**Get Folder Information**

*Method*

|Method name|Returns|
|-----------|-------|
|getfolder|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid api_key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943||
|folderid|The ID of the folder you want to retrieve information for|String|yes*|1|Either folderid and/or foldername must be provided.Available from Razuna version 1.6.6 onwards.|
|foldername|Full or partial name of the folder(s) you wish to retrieve information for.All folders matching the folder name criterion will be returned.|String|yes*|pictures|Either folderid and/or foldername must be provided.Available from Razuna version 1.6.6 onwards.| 

*Output Value*

|Name|Description|Sample Output|Note|
|----|-----------|-------------|----|	
|folder_id|The folderid you passed to this method|1||
|folder_related_to|To which folder this folder is related to|if this is the root folder it will be the same ID as the folder id||
|folder_name|Name of this folder|Renderings||
|folder_description|Folder description|Upload folder|Razuna 1.5.5 (hosted edition 12.11.2012)|
|folder_shared|Depicts whether folder is shared or not|true|Available from Razuna version 1.6.6 onwards.|
|group_permission|An array of groups and related permissions for folder. Groupid '0' is the 'Everybody' group.|[["73CCC1DB-C9A2-445A-B0F3CE28F8780B02","X"],["FDE74B74-D5F5-40F3-A9731BC28D14BB1D","W"],["0","R"]].|Available from Razuna version 1.6.6 onwards. |
|totalassets|Total of all assets in this folder|8||
|totalimg|Total of all assets in this folder|5||
|totalvid|Total of all assets in this folder|2||	
|totaldoc|Total of all assets in this folder|1||
|totalaud|Total of all assets in this folder|3||

*REST: Sample Request*

```
/global/api2/folder.cfc?method=getfolder&api_key=54592180-7060-4D4B-BC74-2566F4B2F943
&folderid=1
```

*Sample Output*

```
{"columns":["folder_id","folder_related_to","folder_name","totalassets","totalimg","totalvid","totaldoc","totalaud"],"data":[["33D207AF29D1447E931A8210982FC4A3","F08BA46F773647899999E80D2B52EC2C","Demo Folder",170,150,10,10,0]]} 
```

Error rendering macro 'excerpt-include' : null

___

**Create Folder**

*Method*

|Method name|Returns|
|-----------|-------|
|setfolder|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid api_key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|folder_name|Name of folder|String|yes|Test Folder|
|folder_owner|The user id that this folder belongs to. If left blank then the current user is the owner.|String|no|(if not passed uses the current user id)|
|folder_related|The ID of the related folder. Important if you create a folder in a sublevel.|String|no|1|
|folder_collection|Is this folder a collection folder|String|no|true ; false (default)|
|folder_description|Description of folder|String|no|This folder is created with the API|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|Response|A result code with the status of the login. If the result is 0 the method was successful.|0|
|folder_id|The ID of the created folder|1|

*REST: Sample Request*

```
/global/api2/folder.cfc?method=setfolder&api_key=54592180-7060-4D4B-BC74-2566F4B2F943
&folder_name=Test Folder
```

*Sample Output*	

```
{["ResponseCode":"0","folder_id":"1"]} 
```
___

**Delete Folder**

> *This method will remove the folder, any sub-folders and content within! There is no way to redo this action !*

*Method*

|Method name|Returns|
|-----------|-------|
|removefolder|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid api key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|folder_id|Name of folder|String|yes|454329579845097425097|	

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|Response|A result code with the status of the login. If the result is 0 the method was successful.|0|
|Message|Message|Folder and content has been successfully removed!|

*REST: Sample Request*

```
/global/api2/folder.cfc?method=removefolder&api_key=54592180-7060-4D4B-BC74-2566F4B2F943
&folder_id=948792317459725198
```	

*Sample Output*

```
{["ResponseCode":"0","message":"Folder and all content within has been successfully removed."]}
```
___

**Set folder permissions**

*Method*

|Method name|Returns|
|-----------|-------|
|setFolderPermissions|String|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid API key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|permissions|JSON Structure|String|yes|JSON structure. See example below|


*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|responsecode|Responsecode|0 (if successful)|
|message|Status Message|Folder permissions successfully updated|

*JSON structure*

*You pass the values for the permissions as a JSON structure. The order is:*

|Nanme|Description||
|-----|-----------|---------|
|folderid|ID of the folder||
|groupid|ID of the group|**The "EVERYBODY" group has the ID of "0" (zero)!**|
|permission|R = read only ; W = read/write ; X = full add |
	
*A example of passing the values would be (you need to serialize your array in order to pass it in a URL):*

```
[["255F307E-AE5A-4E66-AD2F6BBE81D0541C", "13E33EB4-4A82-4CF7-B1DAA549DA80E86B", "X"]]
```

*With CFML you can use the following code snippet to create the JSON (The below code will create a 2 dimensional array and using 2 groups).*

```
<cfset j = arrayNew(2)>
<cfset j[1][1] = "EA4191FB6E0F40D2AFE3ABB85E41118A">
<cfset j[1][2] = "13E33EB4-4A82-4CF7-B1DAA549DA80E86B">
<cfset j[1][3] = "X">
<cfset j[2][1] = "EA4191FB6E0F40D2AFE3ABB85E41118A">
<cfset j[2][2] = "8931CF69-7FB1-476D-9D2B00F63D9D439A">
<cfset j[2][3] = "W">
 
<cfset j = SerializeJSON(j)>
```

*REST: Sample Request*

```
/global/api2/folder.cfc?method=setFolderPermissions&api_key=CA1EBCFD45084E3991EA569DB10A29AA&permissions=[["255F307E-AE5A-4E66-AD2F6BBE81D0541C", "13E33EB4-4A82-4CF7-B1DAA549DA80E86B", "X"]]
```

*Sample Output*

```
{["responsecode":"0","message":"Folder permissions successfully added"]}
```
___

### Collection API2

**Get a list of Collections**

*This method will return all collections within a collection "folder". To iterate for sub-collections you will need to call this method each time.*

*Method*

|Method name|Returns|
|-----------|-------|
|getcollections|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input||
|---------|-----------|----|--------|------------|------------|
|api_key|A valid api key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943||
|folderid|The ID of the collection folder you want to retrieve collections from.|String|yes|2 As of Razuna 1.5.5 you can also pass in a list of folderid's like: 1,34,234|Razuna 1.5.5 Hosted Edition since 16.12.2012|
|released|Query collections according to released status|String|no|Empty value (default)true false|Razuna 1.5.5 Hosted Edition since 10.03.2012 |

*Output Value*

|Name|Description|Sample Output||
|----|-----------|-------------|----------|
|col_id|ID of the collection|212||
|change_date|Date of the last change to this collection|||
|col_name|Name of collection|My collection||
|collection_description|Description|My collection description|Razuna 1.5.5 (hosted edition 12.11.2012)|
|collection_keywords|Keywords|My keywords|Razuna 1.5.5 (hosted edition 16.12.2012)|
|col_released|Status of release|true|Razuna 1.5.5 (hosted edition 10.03.2012)|
|col_copied_from|If copied parent collection ID|108|Razuna 1.5.5 (hosted edition 10.03.2012)|
|totalassets|How many assets are in this collection|8||
|totalaimg|How many images are in this collection|5||
|totalavid|How many videos are in this collection|2||
|totaladoc|How many documents are in this collection|1||
|totalaud|How many audios are in this collection|3||

*REST: Sample Request*

```
/global/api2/collection.cfc?method=getcollections&api_key=54592180-7060-4D4B-BC74-2566F4B2F943
&folderid=1
```

*Sample Output*

```
{"columns":["col_id","change_date","col_name","totalimg","totalvid","totaldoc","totalaud","totalassets"],"data":[["DF45F1F8307A4B92A4EF5FB09001AFE1","January,
 30 2012 00:00:00","chakra
collection",0,0,0,0,0],["A6CE649FAA5F434EB513CA15656AB5AA","March, 15
2012 00:00:00","Marketing Material March
2012",2,1,2,0,5]]} 
```

> **Output format** :*Remember you can adjust the output dynamically. The API returns JSON by default. For record sets it defaults to a ROW based set, if you need COLUMNS simply append "&__BDQUERYFORMAT=column" to your call. In case, you need JSONP you want to append "&__BDRETURNFORMAT=jsonp&callback=?". In order to retrieve XML (WDDX) you simply need to append "&__BDRETURNFORMAT=wddx".*

___

**Retrieving all assets in a collection**

*Method*

|Method name|Returns|
|-----------|-------|
|getassets|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|api_key|A valid api_key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|collectionid|The ID of the collection you want to retrieve assets from.|String|yes|1|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|	
|Response|A result code with the status of the login. If the result is 0 the method was successful.|0|
|calledwith|The collection id you called this method|1|
|totalassetscount|How many assets are in this folder|8|
|different value fields|Each record with is lists|see sample output|

> **Updates** : *As of Razuna 1.5.5 (hosted edition since 30.01.2013) the additional column "rendition_id" and "rendition_url" are being returned, also.*

*REST: Sample Request*

```
/global/api2/collection.cfc?method=getassets&api_key=54592180-7060-4D4B-BC74-2566F4B2F943
&collectionid=234
```

*Sample Output*

```
{"columns":["id","filename","folder_id","extension","extension_thumb","video_image","size","width","height","filename_org","kind","description","keywords","path_to_asset","cloud_url","cloud_url_org","subassets","local_url_org","local_url_thumb","responsecode","totalassetscount","calledwith","rendition_id","rendition_url"],"data":[["5DBE0927C6AA4212B0001930C0F7D7A5","01.14.12
 Affliction LA Lookbook
36475-Edit.tif","4564659C48B348C7B5DAF95AE6C3854E","jpg","jpg","dummy","65493",550,549,"2.jpg","img","","This
 is a
demo","4564659C48B348C7B5DAF95AE6C3854E/img/5DBE0927C6AA4212B0001930C0F7D7A5","","","true","http://localhost:8080/assets/1/4564659C48B348C7B5DAF95AE6C3854E/img/5DBE0927C6AA4212B0001930C0F7D7A5/2.jpg","http://localhost:8080//assets/1/4564659C48B348C7B5DAF95AE6C3854E/img/5DBE0927C6AA4212B0001930C0F7D7A5/thumb_5DBE0927C6AA4212B0001930C0F7D7A5.jpg","0",4,"c-BEF59DE2E65B4709993FDCE6C5E1D818","34941591005E44BEAE6AFE8D8EC6B89E","http://localhost:8080/assets/1/3C05DA46FA184E4F98E2A93FC7B3FFDA/img/34941591005E44BEAE6AFE8D8EC6B89E/hn2_34941591005E44BEAE6AFE8D8EC6B89E.tif"]]}
```

> **Output Format** : *Remember you can adjust the output dynamically. The API returns JSON by default. For record sets it defaults to a ROW based set, if you need COLUMNS simply append "&__BDQUERYFORMAT=column" to your call. In case, you need JSONP you want to append "&__BDRETURNFORMAT=jsonp&callback=?". In order to retrieve XML (WDDX) you simply need to append "&__BDRETURNFORMAT=wddx".*
___

**Search**

> **Availability** : *Search for collections is available as of Razuna 1.5.5 and on the Hosted Edition as of 16.12.2012! As of Razuna 1.5.5 (hosted edition since 16.12.2012) the column "colid" holds the collection ID(s) the file might be in.*

*Method*

|Method name|Returns|
|-----------|-------|
|search|Record set|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|	
|api_key|A valid api_key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|id|ID of a collection|String|no|1|
|name|Name|String|no|my collection|
|description|Description|String|no|my description|
|keyword|Keyword|String|no|my keyword|
|released||String|no|true false|

*(Name, description and keywords searches will be made as "wildcard" searches. Technically, a SQL LIKE and adding "%")*

*Output Value*

The search will return the exact output as the [getcollection() method](http://wiki.razuna.com/display/ecp/Collection+API2#CollectionAPI2-GetalistofCollections)!

*REST: Sample Request*

```
/global/api2/collection.cfc?method=search&api_key=54592180-7060-4D4B-BC74-2566F4B2F943&name=mycol
```
> **Output format** : *Remember you can adjust the output dynamically. The API returns JSON by default. For record sets it defaults to a ROW based set, if you need COLUMNS simply append "&__BDQUERYFORMAT=column" to your call. In case, you need JSONP you want to append "&__BDRETURNFORMAT=jsonp&callback=?". In order to retrieve XML (WDDX) you simply need to append "&__BDRETURNFORMAT=wddx".*
	
___

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
___

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
___

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
___
	
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
___

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
___
	
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
___

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



	



	




	



