**Search API1**

*To retrieve assets from one specific folder you call the folder namespace.*

> **Regarding SessionToken** : *You need to have a valid SessionToken to be able to request any method here*

> **Razuna SaaS Platform** : *If you are accessing assets stored on the Razuna SaaS Platform then make sure those assets are shared, otherwise you will not have any results.*

   * Search
       * Search and finding assets
           * Method
           * Input Parameter
           * Output Value
           * SOAP: Sample Request
           * REST: Sample Request
           * Sample Output

___

**Search and finding assets**

*Method*

|Method Name|
|-----------|
|searchassets|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|sessiontoken|A valid sessiontoken|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|searchfor|The search entry. Same search syntax as in [Search and Find Assets](/user/User Guide/#quick-search) applies.|String|yes|Value to search Enter nothing and all assets will be retrieved|
|offset|This request supports paging. Enter the offset here.|Numeric|yes|0|
|maxrows|The maximum rows you want to request.|Numeric|yes|25 = show 25 assets ; 0 = show ALL assets|
|show|What kind of assets to show|String|yes|all = All assets ; img = Images only ; vid = Videos only ; doc = Documents only ; aud = Audios only|
|doctype|Filters the doc type. Only applies if "show" is set to "doc"!|String|yes|pdf = PDF ; xls = Excel ; doc = Word ; other = All other types ; empty = All doc types|

> *The **offset** and the **maxrows** values are the same as the LIMIT option of the MySQL database. You enter the page (offset) and the amount of records you want to request.Example; There are 125 assets in a folder and you want to return 50 assets then your offset and maxrows would look like; offset=0&maxrows=50. For the next 50 assets you would use; offset=1&maxrows=50 to get to page 2 and so on.*

> **Note :** *To return **all** records, you need to give maxrows a value of 0 (zero)!*

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|Response|A result code with the status of the login. If the result is 0 the method was successful.|0|
|listassets|The body node of the returned list of assets||
|totalassetscount|How many assets are in this folder|8|
|assets|For each asset a asset node is returned with information of the asset|see sample output|

*SOAP: Sample Request*

```
search assets = new search();
string assetlist = assets.searchassets(sessiontoken, searchfor, offset, maxrows, show, doctype);
```
	
*REST: Sample Request*

```
/global/api/search.cfc?method=searchassets&sessiontoken=54592180-7060-4D4B-BC74-2566F4B2F943
&searchfor=batman*&offset=0&maxrows=25&show=all&doctype=
```

*Sample Output*

```
<?xml version="1.0" encoding="UTF-8"?>
<Response>
<responsecode>0</responsecode>
<listassets>
<totalassetscount>6</totalassetscount>
<asset>
<kind>img</kind>
<id>782</id>
<filename>060815002.jpg</filename>
<extension>jpg</extension>
<description>This is a description</description>
<keywords>some,keywords,here</keywords>
<folderid>3</folderid>
<url>http://razunabd.local:8080/assets/1/3/img/782/060815002.jpg</url>
</asset>
<asset>
<kind>doc</kind>
<id>1002</id>
<filename>11g.pdf</filename>
<extension>pdf</extension>
<description/>
<keywords/>
<folderid>1</folderid>
<size>43534</size>
<width>560</width>
<height>240</height>
<url>http://razunabd.local:8080/assets/1/1/doc/1002/11g.pdf</url>
</asset>
</listassets>
</Response>
```

	



