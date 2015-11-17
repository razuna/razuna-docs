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
