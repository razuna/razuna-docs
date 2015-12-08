**Release Notes for Razuna 1.4.1**

**Important Notes for this release**

For Razuna 1.4.1 we changed how we store the paths to the 3rd party libraries. Where as previously, we stored these paths for each hosts individually, we now changed it to a central place. This will make it much easier for organizations that have multiple hosts.

Unfortunately there is no automatic way to fill these values. Thus after upgrading to Razuna 1.4.1 you will see a warning that your libraries can not be found. Simply reenter the paths to the libraries to solve this.

___

**Before moving to Razuna 1.4.1 run the "Update & Export" script**

Error rendering macro 'excerpt-include' : No link could be created for 'Update and Export Script'.

___

**[All resolved issues of Razuna 1.4.1](http://issues.razuna.com/secure/IssueNavigator.jspa?reset=true&jqlQuery=fixVersion%20=%20%221.4.1%22%20AND%20project%20=%20RAZ%20ORDER%20BY%20issuetype%20DESC,%20key%20DESC&tempMax=1000&src=confmacro) (45 issues)**

|Summary|Type|
|-------|----|
|[Option to recreate thumbnail from existing video or image ](http://issues.razuna.com/browse/RAZ-688?src=confmacro)  |New Feature   |
|[Move Collections in dedicated tab ](http://issues.razuna.com/browse/RAZ-681?src=confmacro)  |New Feature   |
|[Better image RAW handling ](http://issues.razuna.com/browse/RAZ-680?src=confmacro)  |New Feature   |
|[Having a central setting for third party libraries](http://issues.razuna.com/browse/RAZ-679?src=confmacro)  |New Feature   |
|[Add F4V as recognized video extension ](http://issues.razuna.com/browse/RAZ-678?src=confmacro)  |New Feature   |
|[Upgrade uploader to 1.3](http://issues.razuna.com/browse/RAZ-677?src=confmacro)  |New Feature   |
|[Show Memory allocation in the Administration and inform user if low ](http://issues.razuna.com/browse/RAZ-653?src=confmacro)  |New Feature   |
|[Ugrade to official OpenBD 1.4 release ](http://issues.razuna.com/browse/RAZ-645?src=confmacro)  |New Feature  |
|[Option to export/import to a SQL script file ](http://issues.razuna.com/browse/RAZ-637?src=confmacro)  | New Feature  |
|[Adding all the RAW image extensions so Razuna can recognize them ](http://issues.razuna.com/browse/RAZ-635?src=confmacro)  | New Feature  |
|[Pages numbers for folder view ](http://issues.razuna.com/browse/RAZ-626?src=confmacro)  |  New Feature |
|[Have a register user link on front page for new users ](http://issues.razuna.com/browse/RAZ-459?src=confmacro)  | New Feature  |
|[Improve error reporting ](http://issues.razuna.com/browse/RAZ-369?src=confmacro)  | New Feature   |
|[Change the preview image for an uploaded file ](http://issues.razuna.com/browse/RAZ-359?src=confmacro)  | New Feature  |
|[View options for Folders and Collections ](http://issues.razuna.com/browse/RAZ-248?src=confmacro)  | New Feature  |
|[Ship Razuna with Tomcat 7 ](http://issues.razuna.com/browse/RAZ-693?src=confmacro)  | Improvement  |Improvement|
|[Adjusted parameters for Amazon S3 validation ](http://issues.razuna.com/browse/RAZ-692?src=confmacro)  | Improvement  |
|[Moving adding of users to a more prominent position in the Admin ](http://issues.razuna.com/browse/RAZ-675?src=confmacro)  | Improvement  |
|[Upgrade jQuery and jQuery UI ](http://issues.razuna.com/browse/RAZ-674?src=confmacro)  | Improvement  |
|[Under rare circumstances (extrem high load and concurrent access) unique id's could not be generated ](http://issues.razuna.com/browse/RAZ-671?src=confmacro)  |Improvement   |

Showing 20 out of [45 issues](http://issues.razuna.com/secure/IssueNavigator.jspa?reset=true&jqlQuery=fixVersion%20=%20%221.4.1%22%20AND%20project%20=%20RAZ%20ORDER%20BY%20issuetype%20DESC,%20key%20DESC&tempMax=1000&src=confmacro)