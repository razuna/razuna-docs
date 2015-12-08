**Release Notes for Razuna 1.5.2**

**Important Notes for this release**

Razuna 1.5.2 is a enhancement and bug fix release which contains 31 issues.

Some of the notable bug fixes are; users were not able to use "search in a search" or search according the date, folder settings for collections was accidentally removed, uploading a PDF could fail under some circumstances and some listing wasn't properly refreshed due to the caching. Among the 20 fixes is a bug that was introduced in 1.5.1 when using MySQL and a hangup on the first time installation. Additionally, users of MS SQL would also run into issues some database issues.  

Our tradition to not only release a version with only bug fixes also holds for Razuna 1.5.2. Thus we are happy to include the following enhancements;

 * The label browser only shows the files that users have access too (finally)

 * Converting RAW images files has been improved (thanks to the many reports)

 * Support for MXF videos and also option to convert into MXF video format
 
 * The API can now handle very large file uploads (tested with >40GB files)

Please take a look at the list below for the complete list if enhancements and bug fixes for Razuna 1.5.2.

___

**How to upgrade**

You should update to 1.5 before updating to 1.5.2! If you have already done so, then simply follow the [Razuna Update Guide](/installation/Upgrade/).

If you are skipping certain version then please make sure to read up on the release notes on each version. There might be instructions for certain updates!

___

**[All resolved issues of Razuna 1.5.2](http://issues.razuna.com/secure/IssueNavigator.jspa?reset=true&jqlQuery=fixVersion+%3D+%221.5.2%22+AND+project+%3D+RAZ+ORDER+BY+%22summary%22+ASC%2Cissuetype+DESC%2C+key+DESC&tempMax=1000&src=confmacro) (36 issues)**

|Summary|Type|
|-------|----|
|[API2: The getasset() method returns the dateadd and datechange columns now ](http://issues.razuna.com/browse/RAZ-1534?src=confmacro)|  Improvement  |
|[API: getfolder() method would throw an error because of missing session ](http://issues.razuna.com/browse/RAZ-1544?src=confmacro)| Bug |
|[Add "action with select" and batch operations to search results ](http://issues.razuna.com/browse/RAZ-587?src=confmacro)| New Feature |
|[Add suggestions for search ](http://issues.razuna.com/browse/RAZ-293?src=confmacro)| New Feature |
|[Asset could be moved into "read-only" folders ](http://issues.razuna.com/browse/RAZ-1549?src=confmacro)| Bug |
|[Cache was not refreshed when files have been converted ](http://issues.razuna.com/browse/RAZ-1565?src=confmacro)| Bug |
|[Changed the download function within Razuna ](http://issues.razuna.com/browse/RAZ-1547?src=confmacro)| Improvement |
|[Checkbox was not selectable anymore due to the new selection with the mouse ](http://issues.razuna.com/browse/RAZ-1552?src=confmacro)| Bug |
|[Cloud Storage: Linking to preview did not work as expected ](http://issues.razuna.com/browse/RAZ-1533?src=confmacro)| Bug |
|[Collections: Folder settings were accidentally removed ](http://issues.razuna.com/browse/RAZ-1560?src=confmacro)|Bug  |
|[Custom Field only for assets (not users) ](http://issues.razuna.com/browse/RAZ-2202?src=confmacro)|Bug  |
|[Enhancements how RAW images are being handled on convert ](http://issues.razuna.com/browse/RAZ-1564?src=confmacro)|Improvement  |
|[Files linked to an external URL have now all metadata fields available. On cloud storage we removed a status message ](http://issues.razuna.com/browse/RAZ-1539?src=confmacro)| Improvement |
|[Fixed an issue which could interfere with the normal operation without plugins ](http://issues.razuna.com/browse/RAZ-1556?src=confmacro)|Bug  |
|[Group count for Administrator group is wrong ](http://issues.razuna.com/browse/RAZ-1559?src=confmacro)|Bug  |
|[Improvements to code and DB to work with large uploads from the API ](http://issues.razuna.com/browse/RAZ-1536?src=confmacro)| Improvement |
|[Labels: Only files are being shown from folders that the user has access too ](http://issues.razuna.com/browse/RAZ-1546?src=confmacro)| Improvement |
|[MXF video support ](http://issues.razuna.com/browse/RAZ-1566?src=confmacro)| Improvement |
|[Metaform generator adds custom fields twice ](http://issues.razuna.com/browse/RAZ-1897?src=confmacro)| Bug |
|[Mini/Mobile browser: small issue could afflict some users opening the browser for the first time ](http://issues.razuna.com/browse/RAZ-1550?src=confmacro)| Bug |

Showing 20 out of [36 issues](http://issues.razuna.com/secure/IssueNavigator.jspa?reset=true&jqlQuery=fixVersion+%3D+%221.5.2%22+AND+project+%3D+RAZ+ORDER+BY+%22summary%22+ASC%2Cissuetype+DESC%2C+key+DESC&tempMax=1000&src=confmacro)











