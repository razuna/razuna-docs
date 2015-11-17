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

   * [Upload API2](/api/Upload API2)
   * [Search API2](/api/Search API2)
   * [Asset API2](/api/Asset API2)
   * [Folder API2](/api/Folder API2)
   * [Collection API2](/api/Collection API2)
   * [Label API2](/api/Label API2)
   * [Custom Fields API2](/api/Custom Fields API2)
   * [User API2](/api/User API2)
   * [Group API2](/api/Group API2)
   * [Hosts API2](/api/Hosts API2)
   * [Comment API2](/api/Comment API2)
   * [Basket API2](/api/Basket API2)
___




	



	




	



