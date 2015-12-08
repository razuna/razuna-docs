**Release Notes for Razuna 1.6.2**

**Important Notes for this release**

Razuna 1.6.2 is a bug fix release. Please note that it is recommended that you re-build your search index. To do so, simply create a scheduled task and choose to rebuild the search index. Please make sure that you only select to rebuild the search index **ONE TIME**!

Please make sure that you not only upgrade the Razuna application, but also take the time to upgrade all 3rd party tools to the latest version as well.

___

**How to upgrade**

You should update to 1.5.2 before updating to 1.6! If you have already done so, then simply follow the [Razuna Update Guide](/installation/Upgrade/).

If you are skipping certain version then please make sure to read up on the release notes on each version. There might be instructions for certain updates!

___

**All resolved issues of Razuna 1.6.2**

|Summary|Type|
|-------|----|
|[Test Search for Lucene 4.6](http://issues.razuna.com/browse/RAZ-2511?src=confmacro)| Technical task  |
|[Option to let users download with their custom filename](http://issues.razuna.com/browse/RAZ-2519?src=confmacro)| New Feature  |
|[Label Drop-Down Pagination](http://issues.razuna.com/browse/RAZ-2472?src=confmacro)|  New Feature  |
|[API: Label API - Search for label ](http://issues.razuna.com/browse/RAZ-2471?src=confmacro)|   New Feature |
|[User account overwritten when logged in to both API requests and Razuna with the same browser ](http://issues.razuna.com/browse/RAZ-2228?src=confmacro)|  New Feature  |
|[Tweak labels to only show the 'Select Labels' feature if more than 200 labels](http://issues.razuna.com/browse/RAZ-2714?src=confmacro)| Improvement  |
|[Refine search by escaping special characters ](http://issues.razuna.com/browse/RAZ-2707?src=confmacro)| Improvement  |
|[Remove alpha channel for previews ](http://issues.razuna.com/browse/RAZ-2515?src=confmacro)| Improvement  |
|[LDAP: Adding scope="subTree" for broader compatibility ](http://issues.razuna.com/browse/RAZ-2507?src=confmacro)|  Improvement |
|[Search: Quick Search supports whole search and finds exact records better now ](http://issues.razuna.com/browse/RAZ-2468?src=confmacro)|  Improvement |
|[API: getRendition() method doesn't need assettype anymore ](http://issues.razuna.com/browse/RAZ-2466?src=confmacro)| Improvement  |
|[Search indexing: Better management of memory and resources during indexing ](http://issues.razuna.com/browse/RAZ-2465?src=confmacro)| Improvement  |
|[Search: Schedule task puts now less strain on server during indexing ](http://issues.razuna.com/browse/RAZ-2458?src=confmacro)| Improvement  |
|[Cannot change folder settings ](http://issues.razuna.com/browse/RAZ-2713?src=confmacro)| Bug  |
|[Indexing a file in linked folder throws error](http://issues.razuna.com/browse/RAZ-2709?src=confmacro)| Bug  |
|[Extended metadata fields when selected to display for files throws error ](http://issues.razuna.com/browse/RAZ-2696?src=confmacro)| Bug  |
|[Backup database in administration throws error ](http://issues.razuna.com/browse/RAZ-2545?src=confmacro)| Bug  |
|[Creating sub-folder of "My Folder" does not work for non-Administrator user ](http://issues.razuna.com/browse/RAZ-2544?src=confmacro)| Bug  |
|[Error when deleting assets individually using the 'Delete Permanently' feature ](http://issues.razuna.com/browse/RAZ-2524?src=confmacro)| Bug  |
|['+' signs in search criterion are removed when call is made via search API ](http://issues.razuna.com/browse/RAZ-2523?src=confmacro)| Bug  |

 Showing 20 out of [57 issues](http://issues.razuna.com/secure/IssueNavigator.jspa?reset=true&jqlQuery=fixVersion+%3D+%221.6.2%22+AND+project+%3D+RAZ+ORDER+BY+issuetype+DESC%2C+key+DESC&src=confmacro) 
