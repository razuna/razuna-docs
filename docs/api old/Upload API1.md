**Upload API1**

*With the below description you can upload assets to your Razuna installation remotely.*

> **Regarding SessionToken** : *You need to have a valid SessionToken to be able to request any method here*

   * Upload
       * Uploading assets remotely
           * URL
           * Input Parameter
           * Output Value
           * Sample Form

___

**Uploading assets remotely**

*Uploading assets within your application has to actually happen with posting the asset to the Razuna web service. The http protocol allows a multipart/form-data POST (RFC 1867) to upload files. You have to pass the required parameters in the form data. These must precede any multipart form data which contains file content. This allows us to verify security before attempting to accept the upload, if this is not done you will receive an error.*

*The maximum content size is limited to the maximum content-length in the http request which is: 2GB (2097150 kilobytes). If you exceed the maximum value you get a 10001 error.*

*URL*

|URL|
|---|
|[http://localhost:8080/razuna/demo/dam/index.cfm](http://localhost:8080/razuna/demo/dam/index.cfm)|


> *You need to adjust the above URL to your installation. Example: For the Hosted platform your URL would be "http://api.razuna.com/index.cfm"*

*Input Parameter*

|Parameter|Description|Type|Required|Sample Input|Version|
|---------|-----------|----|--------|------------|-------|
|fa|required parameter|String|yes|c.apiupload||
|sessiontoken|A valid sessiontoken|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943||
|destfolderid|The folder you want to store the asset in|Numeric|yes|1||
|filedata|The name of the file field|string|yes|This field has to be named "filedata" !||
|zip_extract|To extract a ZIP archive after uploading or not|boolean|no|0 = false ; 1 = true||
|debug|If you turn debug on you will receive an email with the values you are passing to the API|boolean|no|0 = false ; 1 = true||
|emailto|Enter your eMail address in order to receive the debug email|string|no|valid email||
|redirectto|A full URL where to redirect the output of the upload|string|no|[http://razuna.domain.com/index.html](http://razuna.domain.com/index.html).You will get a response with "responsecode=(0)&message=(status message)&assetid=(asset id)"|Razuna 1.4.4 adds the assetid return parameter|
|redirecttoparams|Additional parameters you would like to pass to the "redirectto" string above|string|no|param1=value1&param2=value2 These parameters will get added to the redirectto string "responsecode=(0)&message=(status message)&assetid=(asset id)&param1=value1&param2=value2" Note: Don't add the first "&" as the system will do this automatically|Razuna 1.4.4|
|metadata|Set this to 1 to add metadata during upload. Please note important information below!|boolean|no|0 = false ; 1 = true|Razuna 1.4.5|
|meta_lang_id_r|Set the language you want to write the metadata for. Mandatory if you want to write metadata!|numeric|no|1 = English ; 2 = German ; etc|Razuna 1.4.5|

> *In every Razuna installation there is a default folder called "UploadBin" which has the ID 1.*

> **How to add metadata to your asset during upload** : *As of Razuna 1.4.5 you can populate the metadata fields during the upload. For this to work you need to add the field "metadata" to your post with the value "1". Furthermore, you need to prefix each metadata field with "meta_".*

```
Example: Populate the description, keywords and the location metadata:
meta_img_description = "My description"
meta_img_keywords = "razuna, image, eyes"
meta_location = "New York"
meta_lang_id_r = 1
```

> **Important** : *You DO NOT need to pass a JSON structure. Razuna reads your form fields automatically!*

*Output Value*

|Name|Description|Sample Output|Note|
|----|-----------|-------------|----|
|Response|A result code with the status of the login. If the result is 0 the method was successful.|0||
|message|Returning message|success or session timeout||
|assetid|The ID of the asset in Razuna|2EC82EE9EF03499FBCA4247D99F026B1|Version 1.4.4|
|filetype|The file type (img = image, vid = video, aud = audio, doc = document, other = other format|img|Version 1.4.4|

*Sample Form*

```
<form action="http://demo.razuna.com/index.cfm" name="up" method="post" enctype="multipart/form-data">
<input type="hidden" name="fa" value="c.apiupload">
<input type="hidden" name="sessiontoken" value="54592180-7060-4D4B-BC74-2566F4B2F943">
<input type="hidden" name="destfolderid" value="1">
<input type="hidden" name="filedata" value="filedata">
<input type="hidden" name="zip_extract" value="1">
 
<input type="file" name="filedata">
 
<input type="submit" value="send it">
</form>
```

> **Flash or Flex** : *If you are using a Flash, Flex or AIR application to upload assets to Razuna you will need to use the URL with parameters since Flash only send the filedata id in the post. So you would use the URL of the form action like: [http://demo.razuna.com/index.cfm?fa=c.apiupload&sessiontoken=54592180-7060-4D4B-BC74-2566F4B2F943&destfolderid=1&zip_extract=1](http://demo.razuna.com/index.cfm?fa=c.apiupload&sessiontoken=54592180-7060-4D4B-BC74-2566F4B2F943&destfolderid=1&zip_extract=1)*