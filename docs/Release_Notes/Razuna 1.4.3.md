**Release Notes for Razuna 1.4.3**

**Important Notes for this release**

Razuna 1.4.3 brings some new features, enhancements and many important bug fixes to the 1.4.2 release. The most important new feature is to be able to setup "Upload templates", which allow you to convert your assets during uploading automatically. Furthermore, you can now move folders back into the root structure and the API will list all converted formats.

Moreover, we updated the libraries behind Razuna, optimized how videos are being added to the system, giving you more feedback during searching and more. Please see the list below for a complete rundown of all the issues done in this release

___

**Upgrade from 1.4.2 only**

You should update to 1.4.2 before updating to 1.4.3! If you have already done so, then simply follow the [Razuna Update Guide](/installation/upgrade/).

___

**[All resolved issues of Razuna 1.4.3](http://issues.razuna.com/secure/IssueNavigator.jspa?reset=true&jqlQuery=fixVersion%20=%20%221.4.3%22%20AND%20project%20=%20RAZ%20ORDER%20BY%20issuetype%20DESC,%20key%20DESC&tempMax=1000&src=confmacro) (23 issues)**

|Summary|Type|
|-------|----|
|[Option to move any folder to the root level ](http://issues.razuna.com/browse/RAZ-752?src=confmacro) |New Feature |
|[API: Add converted formats to getassets method ](http://issues.razuna.com/browse/RAZ-747?src=confmacro) |New Feature |
|[Upload Templates / Auto Convert on upload ](http://issues.razuna.com/browse/RAZ-206?src=confmacro) |New Feature |
|[Update Tomcat to version 7.0.10 for standalone distribution ](http://issues.razuna.com/browse/RAZ-758?src=confmacro) |Improvement  |
|[Update to the backend libraries for OpenBD ](http://issues.razuna.com/browse/RAZ-757?src=confmacro) |Improvement |
|[Check the executable path for the libraries within the administration ](http://issues.razuna.com/browse/RAZ-756?src=confmacro) |Improvement |
|[API: Add height and width for assets (images and videos return these values) ](http://issues.razuna.com/browse/RAZ-751?src=confmacro) |Improvement |
|[Upgrade upload tool to 1.4.2 ](http://issues.razuna.com/browse/RAZ-750?src=confmacro) |Improvement |
|[Feedback on search when there are no records found ](http://issues.razuna.com/browse/RAZ-744?src=confmacro) |Improvement |
|[Optimizing adding of videos ](http://issues.razuna.com/browse/RAZ-738?src=confmacro) |Improvement |
|[Threads for creating a new version have unique ids now ](http://issues.razuna.com/browse/RAZ-737?src=confmacro) |Improvement  |
|[The file size of assets was not calculated properly on server, email and ftp upload ](http://issues.razuna.com/browse/RAZ-754?src=confmacro) |Bug |
|[AP: Calling the API might throw an error since there is a undefined session variable set which was not initiated trough the API calls ](http://issues.razuna.com/browse/RAZ-753?src=confmacro) |Bug |
|[When there is no user access on shared folders it could throw an exception ](http://issues.razuna.com/browse/RAZ-749?src=confmacro) |Bug |
|[Exporting could throw an error because of the deprecated sequences table ](http://issues.razuna.com/browse/RAZ-748?src=confmacro) |Bug |
|[Moving a folder to itself throws an error ](http://issues.razuna.com/browse/RAZ-745?src=confmacro) |Bug |
|[When there were no assets being found during searching the system would throw an error ](http://issues.razuna.com/browse/RAZ-743?src=confmacro) |Bug |
|[Basket download would sometimes throw an error ](http://issues.razuna.com/browse/RAZ-742?src=confmacro) |Bug |
|[Group permissions did not get saved properly for folders ](http://issues.razuna.com/browse/RAZ-741?src=confmacro) |Bug |
|[Javascript while selecting a group within permissions did not execute ](http://issues.razuna.com/browse/RAZ-740?src=confmacro) |Bug |

Showing 20 out of [23 issues](http://issues.razuna.com/secure/IssueNavigator.jspa?reset=true&jqlQuery=fixVersion%20=%20%221.4.3%22%20AND%20project%20=%20RAZ%20ORDER%20BY%20issuetype%20DESC,%20key%20DESC&tempMax=1000&src=confmacro) 

