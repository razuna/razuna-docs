**Release Notes for Razuna 1.4.2**

**Important Notes for this release**

Razuna 1.4.2 brings many important bug fixes to the 1.4.1 release. Especially, for users who are uploading ZIP archives with foreign chars and adding ZIP archives in general. We also could improve the performance on these operations.

Other then that we changed the we way we create backups completely. Now, we store your backups internally and thus avoiding problems users had with migrating large datasets from one server to another and sometimes failing due to charsets (one platform to another) and special chars in the backup file (thus causing the import to fail). 

___

**Before moving to Razuna 1.4.2 run the "Update & Export" script**

Error rendering macro 'excerpt-include' : No link could be created for 'Update and Export Script'.

___

**[All resolved issues of Razuna 1.4.2](http://issues.razuna.com/secure/IssueNavigator.jspa?reset=true&jqlQuery=fixVersion%20=%20%221.4.2%22%20AND%20project%20=%20RAZ%20ORDER%20BY%20issuetype%20DESC,%20key%20DESC&tempMax=1000&src=confmacro) (30 issues)**

|Summary|Type|
|-------|----|
|[Update to Lucene 3.0.3 ](http://issues.razuna.com/browse/RAZ-725?src=confmacro)|Improvement  |
|[Improvement for database backup and restore ](http://issues.razuna.com/browse/RAZ-720?src=confmacro)|Improvement  |
|[Update internal database to 1.2.47 ](http://issues.razuna.com/browse/RAZ-719?src=confmacro)|Improvement  |
|[Adding global system information to the system settings panel ](http://issues.razuna.com/browse/RAZ-718?src=confmacro)|Improvement  |
|[New id system ](http://issues.razuna.com/browse/RAZ-716?src=confmacro)|Improvement  |
|[Speed improvements during adding of assets especially during when processing zip archives ](http://issues.razuna.com/browse/RAZ-715?src=confmacro)|Improvement  |
|[Improved the way folders and assets are being removed ](http://issues.razuna.com/browse/RAZ-714?src=confmacro)|Improvement  |
|[Adjusting asset view to fit asset dynamically to the size of the browser. Adjusting for smaller screen also. ](http://issues.razuna.com/browse/RAZ-710?src=confmacro)|Improvement  |
|[Design changes for floating boxes ](http://issues.razuna.com/browse/RAZ-708?src=confmacro)|Improvement  |
|[Fix for some small design issues ](http://issues.razuna.com/browse/RAZ-703?src=confmacro)|Improvement  |
|[Removed unnecessary path to third party tools in adding a new hosts (they are globally stored) ](http://issues.razuna.com/browse/RAZ-700?src=confmacro)|Improvement  |
|[Removed unnecessary details from host details ](http://issues.razuna.com/browse/RAZ-699?src=confmacro)|Improvement  |
|[The Admin did not automatically refresh on changes ](http://issues.razuna.com/browse/RAZ-698?src=confmacro)|Improvement  |
|[Adding a host name with spaces did not correctly verify ](http://issues.razuna.com/browse/RAZ-697?src=confmacro)|Improvement  |
|[Login with different users could sometimes still show folders and permissions from another user ](http://issues.razuna.com/browse/RAZ-726?src=confmacro)|Bug |
|[Upload to FTP cant find arguments.thestruct.dynpath ](http://issues.razuna.com/browse/RAZ-724?src=confmacro)|Bug |
|[Nameless folder from basket mail ](http://issues.razuna.com/browse/RAZ-723?src=confmacro)|Bug |
|[Versioning a video did not work properly ](http://issues.razuna.com/browse/RAZ-713?src=confmacro)|Bug |
|[Extracting a zip archive will now extract all folders and will add them correctly now ](http://issues.razuna.com/browse/RAZ-712?src=confmacro)|Bug |
|[Adding assets from server directory did not work if folder name had spaces ](http://issues.razuna.com/browse/RAZ-711?src=confmacro)|Bug |

Showing 20 out of [30 issues](http://issues.razuna.com/secure/IssueNavigator.jspa?reset=true&jqlQuery=fixVersion%20=%20%221.4.2%22%20AND%20project%20=%20RAZ%20ORDER%20BY%20issuetype%20DESC,%20key%20DESC&tempMax=1000&src=confmacro)