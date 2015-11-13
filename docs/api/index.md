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

###Search API

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

###Asset API


	


	




	




