**Release Notes for Razuna 1.4.4**

**Important Notes for this release**

Razuna 1.4.4 brings some enhancements and many important bug fixes to the 1.4.3 release. In short, we fixed some bugs which affected Windows installations (some users could not add images to the system), also users with a MSSQL server got some unexpected errors due to the new ID system which was introduced in 1.4.2. Windows users will also be happy to see that we fixed bugs with writing the metadata, creating thumbnails and the playback of videos.

Moreover, we also added some enhancements to the video player (which adds compatibility to the latest browser generations) and Administrators see now all folders from all users (and also other Administrators) by default.

Additionally, we made improvements to the search engine. The search provides a visual feedback and we changed the search pattern so that separate words are searched with "AND" (thus adding the words together).

Last but not least, Developers have a reason to celebrate. With Razuna 1.4.4 we are introducing new options to the API. These are;

   * Modify Metadata (Link to the DeveloperGuide)
   * Uploading an asset returns the assetid and the asset type

___

**Upgrade from 1.4.2 only**

You should update to 1.4.2 before updating to 1.4.4! If you have already done so, then simply follow the [Razuna Update Guide](/installation/upgrade/).

___

**[All resolved issues of Razuna 1.4.4](http://issues.razuna.com/secure/IssueNavigator.jspa?reset=true&jqlQuery=fixVersion%20=%20%221.4.4%22%20AND%20project%20=%20RAZ%20ORDER%20BY%20issuetype%20DESC,%20key%20DESC&tempMax=1000&src=confmacro) (25 issues)**

|Summary|Type|
|-------|----|
|[SystemAdmins & Administrators see now all folders of all users by default ](http://issues.razuna.com/browse/RAZ-787?src=confmacro)| Improvement    |
|[Upload Templates: Refresh list when adding or updating ](http://issues.razuna.com/browse/RAZ-784?src=confmacro)| Improvement    |
|[Updated to the latest embedded video and audio player ](http://issues.razuna.com/browse/RAZ-783?src=confmacro)| Improvement    |
|[Administration Login: Show loading status until page is really reloading ](http://issues.razuna.com/browse/RAZ-778?src=confmacro)| Improvement    |
|[The state of showing folders of users or not is now remembered (only applicable for Administrators) ](http://issues.razuna.com/browse/RAZ-775?src=confmacro)| Improvement    |
|[API: Uploading returns the file type ](http://issues.razuna.com/browse/RAZ-773?src=confmacro)| Improvement    |
|[API: Adding additional "redirecttoparams" to the upload api call ](http://issues.razuna.com/browse/RAZ-772?src=confmacro)| Improvement    |
|[API: Uploading returns the assetid ](http://issues.razuna.com/browse/RAZ-771?src=confmacro)| Improvement    |
|[Provide visual feedback on searching ](http://issues.razuna.com/browse/RAZ-768?src=confmacro)| Improvement    |
|[Empty search does now NOT search anymore (previously we returned all records) ](http://issues.razuna.com/browse/RAZ-766?src=confmacro)| Improvement    |
|[Rearrange search to search with AND as soon as there are two or more words in the search term ](http://issues.razuna.com/browse/RAZ-765?src=confmacro)| Improvement    |
|[API: Option to modify meta data ](http://issues.razuna.com/browse/RAZ-331?src=confmacro)| Improvement    |
|[Error Report ](http://issues.razuna.com/browse/RAZ-790?src=confmacro)| Bug  |
|[Upload Templates: Throws an error when saving with nothing selected ](http://issues.razuna.com/browse/RAZ-785?src=confmacro)| Bug  |
|[Videos could not be properly played in the embedded player ](http://issues.razuna.com/browse/RAZ-782?src=confmacro)| Bug  |
|[Inheriting folder permissions is not working ](http://issues.razuna.com/browse/RAZ-781?src=confmacro)| Bug  |
|[Showing the username of each folder correctly now (only applicable to Administrators) ](http://issues.razuna.com/browse/RAZ-780?src=confmacro)| Bug  |
|[Javascript for selecting groups in collection settings did not work properly ](http://issues.razuna.com/browse/RAZ-779?src=confmacro)| Bug  |
|[On Windows the XMP metadata could not be writen to the asset if there was a space in the path ](http://issues.razuna.com/browse/RAZ-777?src=confmacro)|Bug   |
|[MS SQL: Some field types were not aligned to the new ID system ](http://issues.razuna.com/browse/RAZ-776?src=confmacro)|Bug   |

Showing 20 out of [25 issues](http://issues.razuna.com/secure/IssueNavigator.jspa?reset=true&jqlQuery=fixVersion%20=%20%221.4.4%22%20AND%20project%20=%20RAZ%20ORDER%20BY%20issuetype%20DESC,%20key%20DESC&tempMax=1000&src=confmacro)

