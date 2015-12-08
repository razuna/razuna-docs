**Collection API**

> **Regarding SessionToken** : *You need to have a valid SessionToken to be able to request any method here*

   * Collection API
       * Get Collections in a tree
           * Method
           * Input Parameter
           * Output Value
           * SOAP: Sample Request
           * REST: Sample Request
           * Sample Output
           * Sample Output for e4x
       * Get a list of Collections
           * Method
           * Input Parameter
           * Output Value
           * SOAP: Sample Request
           * REST: Sample Request
           * Sample Output
           * Sample Output for e4x
       * Retrieving all assets in a collection
           * Method
           * Input Parameter
           * Output Value
           * SOAP: Sample Request
           * REST: Sample Request
           * Sample Output

___

**Get Collections in a tree**

*This method will return all collections and sub-collections in a tree. Please be aware that with a lot of collections this can put a strain on your Razuna server!*

> **About Collections** : *It's important to understand that Collections are just another "folder" and thus you will have to query the collection "folder" first, then the collections within that and finally the assets within the collection.*

*Method*

|Method Name|
|-----------|
|getcollectionstree|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|sessiontoken|A valid sessiontoken|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|e4x|To return the XML in e4x format or not|Numeric|yes|0 = No ; 1 = yes|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|Response|A result code with the status of the login. If the result is 0 the method was successful.|0|
|listcollections|The body node of the returned list of collections||
|collection|The root element||
|collectionid|ID of the collection|2|	
|collectionname|Name of collection|Demo Collection|
|collectionlevel|Level of this collection|1|
|parentid|Parent ID of this collection|1|
|hassubcollection|Collection contains sub-collection|true or false|
|subcollection|The root element of sub-collection|The sub-collection element may contain all sub-collection with each element of the collection|
|collectionowner|The userid of the owner|8|

*SOAP: Sample Request*

```
collection tree = new collection();
string collectionlist = tree.getcollectionstree(sessiontoken, e4x);
```
	
*REST: Sample Request*

```
/global/api/collection.cfc?method=getcollectionstree&sessiontoken=54592180-7060-4D4B-BC74-2566F4B2F943
&e4x=0
```

*Sample Output*

```
<?xml version="1.0" encoding="UTF-8"?>
<Response>
<responsecode>0</responsecode>
<listcollections>
<collection>
<collectionid>2</collectionid>
<collectionname>Demo Collection</collectionname>
<collectionlevel>1</collectionlevel>
<collectionowner>8</collectionowner>
<parentid>3</parentid>
<hassubcollection>true</hassubcollection>
<subcollection>
<collectionid>12</collectionid>
<collectionname>A subcollection</collectionname>
<collectionlevel>2</collectionlevel>
<parentid>3</parentid>
<hassubcollection>false</hassubcollection>
</subcollection>
</collection>
</listcollections>
</Response>
Sample Output for e4x
<Response>
<responsecode>0</responsecode>
<listcollections>
<collection collectionid="3" collectionname="Demo Collection" collectionlevel="1" parentid="3" hassubcollection="true" collectionowner="8">
<subcollection>
<collection collectionid="12" collectionname="A subcollection" collectionlevel="2" parentid="3" hassubcollection="false" collectionowner="8">
</collection>
</subcollection>
</folder>
</listcollections>
```
___

**Get a list of Collections**

*This method will return all collections within a collection "folder". To iterate for sub-collections you will need to call this method each time.*

*Method*

|Method Name|
|-----------|
|getcollections|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|sessiontoken|A valid sessiontoken|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|folderid|The ID of the collection folder you want to retrieve collections from.|Numeric|yes|2|
|e4x|To return the XML in e4x format or not|Numeric|yes|0 = No ; 1 = yes|

*Output Value*

|Name|Description|Sample Output|Notes|
|----|-----------|-------------|-----|
|Response|A result code with the status of the login. If the result is 0 the method was successful.|0||
|calledwith|The id you called this method|1||
|listcollections|The body node of the returned list of collections|||
|collectionid|ID of the collection|212||
|collectionname|Name of the collection|Demo Collection||
|totalassets|How many assets are in this collection|8|Razuna 1.3.5|
|totalimg|How many images are in this collection|5|Razuna 1.3.5|
|totalvid|How many videos are in this collection|2|Razuna 1.3.5|
|totaldoc|How many documents are in this collection|1|Razuna 1.3.5|
|totalaud|How many audios are in this collection|3|Razuna 1.3.5|

*SOAP: Sample Request*

```
collection list = new collection();
string collectionlist = list.getcollections(sessiontoken, folderid, e4x);
```

*REST: Sample Request*

```
/global/api/collection.cfc?method=getcollections&sessiontoken=54592180-7060-4D4B-BC74-2566F4B2F943
&folderid=0&e4x=0
```

*Sample Output*

```
<?xml version="1.0" encoding="UTF-8"?>
<Response>
<responsecode>0</responsecode>
<calledwith>1</calledwith>
<listcollections>
<collection>
<collectionid>3</collectionid>
<collectionname>Demo Collection</collectionname>
<totalassets>8</totalassets>
<totalimg>5</totalimg>
<totalvid>2</totalvid>
<totaldoc>1</totaldoc>
<totalaud>3</totalaud>
</collection>
</listcollections>
</Response>
```

*Sample Output for e4x*

```
<Response>
<responsecode>0</responsecode>
<calledwith>1</calledwith>
<listcollections>
<collection collectionid="3" collectionname="Demo Collection" totalassets="8" totalimg="5" totalvid="2" totaldoc="1" totalaud="3" />
</listcollections>
```

___

**Retrieving all assets in a collection**

*Method*

|Method Name|
|-----------|
|getassets|

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|
|---------|-----------|----|--------|------------|
|sessiontoken|A valid sessiontoken|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943|
|collectionid|The ID of the collection you want to retrieve assets from.|Numeric|yes|1|

*Output Value*

|Name|Description|Sample Output|
|----|-----------|-------------|
|Response|A result code with the status of the login. If the result is 0 the method was successful.|0|
|calledwith|The collection id you called this method|1|
|totalassetscount|How many assets are in this folder|8|
|listassets|The body node of the returned list of assets||
|assets|For each asset a asset node is returned with information of the asset|see sample output|

*SOAP: Sample Request*

```
collection assets = new collection();
string assetlist = assets.getassets(sessiontoken, collectionid);
```
	
*REST: Sample Request*

```
/global/api/collection.cfc?method=getassets&sessiontoken=54592180-7060-4D4B-BC74-2566F4B2F943
&collectionid=1
```

*Sample Output*

*Error rendering macro 'excerpt-include' : No link could be created for 'Folder'.*
