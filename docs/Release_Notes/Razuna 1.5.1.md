**Release Notes for Razuna 1.5.1**

**Important Notes for this release**

Razuna 1.5.1 was planned to be a maintenance release to Razuna 1.5, but as it turned out we did not wanted to hold back with some of the new stuff we've build in the meantime. Thus, this release introduces a redesigned entry page (with a convenient upload button), a updated folder view and most prominently a redesigned file detail view where all relevant information can be found in one place (place have a look at our [blog post outlining this in more details](http://blog.razuna.com/2012/09/10/user-interface-changes-in-razuna/)). Since we are speaking of design and usability, users can now select the files with the mouse/keyboard in the folder view, the mobile side has been completely redesigned and with this release users of the self-hosted edition can use the recently [released Razuna Google Chrome Extensions](http://blog.razuna.com/2012/09/03/the-all-new-razuna-chrome-extension-is-here/).

Furthermore, we have changed the permissions for "read-only" slightly. This means that "read-only" groups are not able to download the original file anymore, except one sets it to download in the shared options. On the sharing section we now propagate changes from the folder settings to all sub-folders and done some more tweaking to how sharing works.

Razuna 1.5 introduced a new caching engine. Naturally, sometimes the caching was done too much or wasn't refreshed properly. Razuna 1.5.1 fixes this in many parts. Moreover, the API2 is now also using the same caching and thus developers should not see a "delay" anymore in their results from the API.

Last but not least, we have had some issues with connecting to FTP servers. In short, the engine wasn't able to deal with some FTP servers and especially with folder & files that contained spaces or any foreign characters. This release, contains the latest update to the engine which fixed this issue. 

Please take a look at the list below to see some of the latest features, enhancements and bug fixes for Razuna 1.5.1.

___

**How to upgrade**

You should update to 1.5 before updating to 1.51! If you have already done so, then simply follow the [Razuna Update Guide](/installation/Upgrade/).

If you are skipping certain version then please make sure to read up on the release notes on each version. There might be instructions for certain updates!

___

**[All resolved issues of Razuna 1.5.1](http://issues.razuna.com/secure/IssueNavigator.jspa?reset=true&jqlQuery=fixVersion%20=%20%221.5.1%22%20AND%20project%20=%20RAZ%20ORDER%20BY%20issuetype%20DESC,%20key%20DESC&tempMax=1000&src=confmacro) (44 issues)**

|Summary|Type|
|-------|----|
|[Select files with mouse (selectable with mouse lasso effect or with command click) ](http://issues.razuna.com/browse/RAZ-1529?src=confmacro)| New Feature  |
|[Re-designed Google Chrome Extension ](http://issues.razuna.com/browse/RAZ-1505?src=confmacro)|  New Feature |
|[Complete re-design of the mobile Razuna interface ](http://issues.razuna.com/browse/RAZ-1504?src=confmacro)| New Feature  |
|[Add UTF-8 encoding parameters to JDBC string in order to save non-Latin characters successfully ](http://issues.razuna.com/browse/RAZ-1490?src=confmacro)| New Feature  |
|[API2 is using the same cache as Razuna itself now. Should resolve issue with "delays" ](http://issues.razuna.com/browse/RAZ-1531?src=confmacro)| Improvement   |
|[We now list all the available renditions in the download window, but only have links for those who are set to be downloadable ](http://issues.razuna.com/browse/RAZ-1524?src=confmacro)|Improvement    |
|[Change permissions of "read only" users to NOT be able to download originals within Razuna ](http://issues.razuna.com/browse/RAZ-1523?src=confmacro)|Improvement    |
|[If we set "download original" within shared folders or widgets propagate the change to all assets within sub-folders ](http://issues.razuna.com/browse/RAZ-1520?src=confmacro)| Improvement   |
|[API2 more compatible with general structure ](http://issues.razuna.com/browse/RAZ-1515?src=confmacro)|Improvement    |
|[Re-design of entry page ](http://issues.razuna.com/browse/RAZ-1514?src=confmacro)| Improvement   |
|[Due to the engine change for the FTP protocol needed changes ](http://issues.razuna.com/browse/RAZ-1513?src=confmacro)| Improvement   |
|[Combined Edit View is only accessible by users with write permissions ](http://issues.razuna.com/browse/RAZ-1511?src=confmacro)|Improvement    |
|[Re-design of file detail page ](http://issues.razuna.com/browse/RAZ-1510?src=confmacro)| Improvement   |
|[Re-design of folder view and list view ](http://issues.razuna.com/browse/RAZ-1509?src=confmacro)|  Improvement  |
|[Re-design of selections ](http://issues.razuna.com/browse/RAZ-1508?src=confmacro)| Improvement   |
|[Removed Twitter and Facebook from front page ](http://issues.razuna.com/browse/RAZ-1507?src=confmacro)| Improvement   |
|[Better image if we could not generate a thumbnail for a video ](http://issues.razuna.com/browse/RAZ-1506?src=confmacro)| Improvement   |
|[PDF thumbnails take now the same settings for the size as the thumbnail setting for images ](http://issues.razuna.com/browse/RAZ-1502?src=confmacro)| Improvement   |
|[Update to Lucene 3.6.1 ](http://issues.razuna.com/browse/RAZ-1499?src=confmacro)|  Improvement  |
|[When a group is being added/removed for a user, we also flush the search cache without the need for the administrator to flush the database cache ](http://issues.razuna.com/browse/RAZ-1496?src=confmacro)| Improvement   |

Showing 20 out of [44 issues](http://issues.razuna.com/secure/IssueNavigator.jspa?reset=true&jqlQuery=fixVersion%20=%20%221.5.1%22%20AND%20project%20=%20RAZ%20ORDER%20BY%20issuetype%20DESC,%20key%20DESC&tempMax=1000&src=confmacro)
