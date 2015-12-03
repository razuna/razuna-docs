**How to show dedicated Razuna UI parts in your application**

> **Razuna 1.6** : This feature is available since Razuna 1.6!

Developers may want to show the content of a folder or the uploader within their applications to the user. This is now possible with a direct call to the needed UI and the required parameters. Find the available "CUSTOM VIEW" features and its parameters below.

   * Showing the content of a folder
   * Showing the uploader tool only
   * Showing the search results

___

**Showing the content of a folder**

URL and parameters to use:

```
[http://localhost/(razuna/)raz1/dam/index.cfm?fa=c.view_custom&api_key=(apikey)&folderid=(folderid)&showpart=folder&access=r&fileid=108](http://localhost/(razuna/)raz1/dam/index.cfm?fa=c.view_custom&api_key=(apikey)&folderid=(folderid)&showpart=folder&access=r&fileid=108)
```

Parameters

|Parameter|Value|Required|Description|Availability|
|---------|-----|--------|-----------|------------|
|fa|c.view_custom|required|The action to call||
|api_key|(your api key)|required|This is the same API you use for any API call||
|folderid|(folder id)|	required|The folder id to show content from||
|showpart|folder|required|"folder" is the value here in order to show the folder content||
|access|r = read (default) w = read/write x = full access|optional|Pass in the permission you want this files in this folder to appear under.||
|fileid|(file id)|optional|Pass in a fileid or a list of fileids (separated with a comma) in order to only show the files listed.||
|userid|(user id)|optional|Pass in a user id and the view will be shows as the user. Additionally, it will also have the groups of the user assigned!||
|sortby|name  sizedesc  sizeasc  dateadd  datechange|optional|This will sort the folder view according to your passed value.||
|showsubfolders|f = false (default)  t = true  |optional|Shows files from subfolders||
|customparams|Free structure, JSON structure |optional| Pass you own custom parameters to the view. The value will be stored in a session called "session.customparams" and can be retrieved by the very same name. You can store any value in this parameter. For complex objects we recommend to pass a JSON structure.|1.6.5|

The above URL and its given parameters allow you to show the folder content UI in any application (via iFrame or alike). Given the above this will show the below (this is a sample, your might looks differently):

![](/How/img/Screenshot_1_14_13_11_37_AM.png)

___

**Showing the uploader tool only**

URL and parameters to use:

```
[http://localhost/(razuna/)raz1/dam/index.cfm?fa=c.view_custom&api_key=(apikey)&folderid=(folderid)&showpart=upload](http://localhost/(razuna/)raz1/dam/index.cfm?fa=c.view_custom&api_key=(apikey)&folderid=(folderid)&showpart=upload)
```

Parameters

|Parameter|Value|Required|Description|Availability|
|---------|-----|--------|-----------|------------|
|fa|c.view_custom|required|The action to call||
|api_key|(your api key)|required|This is the same API you use for any API call||
|folderid|(folder id)|	required|The folder id of the folder you want to upload into **Instead of a folder id you can also use a "x" here and it will show the list of folder first where the user can choose the folder to upload into**||
|showpart|folder|required|"upload" is the value here in order to show the upload tool||
|userid|(user id)|optional|Pass in a user id and the view will be shows as the user. Additionally, it will also have the groups of the user assigned!||
|customparams|Free structure , JSON structure|optional|Pass you own custom parameters to the view. The value will be stored in a session called "session.customparams" and can be retrieved by the very same name. You can store any value in this parameter. For complex objects we recommend to pass a JSON structure.|1.6.5|

With the given URL and parameter above you will get the content of the uploader tool which you can then embed in your application as shown below:

![](/How/img/Screenshot_1_14_13_11_41_AM.png)

___

**Showing the search results**

URL and parameters to use (Example):

```
[http://localhost/(razuna/)raz1/dam/index.cfm?fa=c.view_custom&api_key=(apikey)&searchfor=audrey&show=all&access=r&showpart=search](http://localhost/(razuna/)raz1/dam/index.cfm?fa=c.view_custom&api_key=(apikey)&searchfor=audrey&show=)
```

Parameters

|Parameter|Value|Required|Description|Availability|
|---------|-----|--------|-----------|------------|
|fa|c.view_custom|required|The action to call||
|api_key|(your api key)|required|This is the same API you use for any API call||
|showpart|search|required|"search" is the value here to show the search results||
|searchfor|search term|required|Enter the search term *see the search API for accepted values||
|access|r = read (default) w = read/write  x = full access|optional|Pass in the permission you want the results to appear under.||
|userid|(user id)|optional|Pass in a user id and the view will be shows as the user. Additionally, it will also have the groups of the user assigned!||
|sortby|name sizedesc sizeasc dateadd datechanged|optional|This will sort the folder view according to your passed value.||
|customparams|Free structure, JSON structure|optional|Pass you own custom parameters to the view. The value will be stored in a session called "session.customparams" and can be retrieved by the very same name. You can store any value in this parameter. For complex objects we recommend to pass a JSON structure.|1.6.5|

> To see all possible parameters that can be used see the [search API](http://wiki.razuna.com/display/ecp/Search+API2) !

This UI component will show you the search results page in its own window like the one below (example):

![](/How/img/Screenshot_3_3_13_4_17_PM.png)



