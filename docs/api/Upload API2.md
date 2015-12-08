###Upload API2

With the below description you can upload assets to your Razuna installation remotely.

*Uploading assets remotely*

Uploading assets within your application has to actually happen with posting the asset to the Razuna web service. The http protocol allows a multipart/form-data POST (RFC 1867) to upload files. You have to pass the required parameters in the form data. These must precede any multipart form data which contains file content. This allows us to verify security before attempting to accept the upload, if this is not done you will receive an error.

The maximum content size is limited to the maximum content-length of a HTTP request. If you exceed the maximum value you get a 10001 error.


Since this is a post directly into Razuna, the URL for this API call differs from the rest. Thus your endpoint will be the index file of your tenant/host. Example: [http://localhost:8080/razuna/raz1/dam/index.cfm](http://localhost:8080/razuna/raz1/dam/index.cfm.) (Obviously you'll need to adjust the URL for your installation).

If you develop on our Razuna Shared Platform your endpoint is your subdomain, e.g [http://demo.razuna.com/index.cfm](http://demo.razuna.com/index.cfm)

 * Input Parameter

|Parameter|Description|Type|Required|Sample Input|Version|
|---------|-----------|----|--------|------------|-------|
|api_key|A valid api_key|String|yes|54592180-7060-4D4B-BC74-2566F4B2F943||
|debug|If you turn debug on you will receive an email with the values you are passing to the API|boolean|no|0 = false (default) 1 = true||
|destfolderid|The folder you want to store the asset in|String|yes|1||
|emailto|Enter your eMail address in order to receive the debug email|string|no|valid email||
|fa|required parameter is "c.apiupload"|String|yes|c.apiupload||
|filedata|The name of the file field (filedata)|File field|yes|This field has to be named "filedata" !||
|meta_lang_id_r|Set the language you want to write the metadata for. Mandatory if you want to write metadata!|numeric|no|1 = English   2 = German   etc.|Razuna 1.4.5   |
|metadata|Set this to 1 to add metadata during upload. Please note important information below!|boolean|no|0 = false (default)  1 = true  |Razuna 1.4.5|
|redirectto|A full URL where to redirect the output of the upload|string|no|[http://razuna.domain.com/index.html](http://razuna.domain.com/index.html) ; You will get a response with "responsecode=(0)&message=(status message)&assetid=(asset id)"|Razuna 1.4.4 adds the assetid return parameter|
|redirecttoparams|Additional parameters you would like to pass to the "redirectto" string above|string|no|param1=value1&param2=value2 ; These parameters will get added to the redirectto string "responsecode=(0)&message=(status message)&assetid=(asset id)&param1=value1&param2=value2" ; Note: Don't add the first "&" as the system will do this automatically|Razuna 1.4.4|
|skip_event|The event name you want to skip (only in combination with the workflow plugin)|String|no|on_pre_process = Pre-Process on_file_add = Add file(s) on_file_edit = Edit file(s) on_file_move = Move file(s) on_file_remove = Delete file(s) on_folder_add = Add folder on_folder_edit = Edit folder on_folder_move = Move folder on_folder_remove = Delete folder  .You can skip many events by separating each event with a comma, e.g. "on_pre_process,on_file_add"|Razuna 1.6|
|upl_template|ID of the upload template to execute|String|no|54592180064BC7466F4B2F943|Razuna 1.6|
|zip_extract|To extract a ZIP archive after uploading or not|boolean|no|0 = false 1 = true (default)||




How to add metadata to your asset during upload

As of Razuna 1.4.5 you can populate the metadata fields during the upload. For this to work you need to add the field "metadata" to your post with the value "1". Furthermore, you need to prefix each metadata field with "meta_". A list of the correct and available metadata fields is available here.
```
Example: Populate the description, keywords and the location metadata:
meta_img_description = "My description"
meta_img_keywords = "razuna, image, eyes"
meta_location = "New York"
meta_lang_id_r = 1
```
Important
You DO NOT need to pass a JSON structure. Razuna reads your form fields automatically!
___
*Output Value*

The below will be returned to you in XML format.

|Name|Description|Sample Output|Note|
|----|-----------|-------------|----|
|Response|A result code with the status of the login. If the result is 0 the method was successful.|0||
|message|Returning message|success||
|assetid|The ID of the asset in Razuna|2EC82EE9EF03499FBCA4247D99F026B1|Version 1.4.4|
|filetype|The file type (img = image, vid = video, aud = audio, doc = document, other = other format|img|Version 1.4.4|
|comingfrom|The HTTP referrer of the request|http://myuploadscript|Version 1.6|
|renamefilebody	|Requests coming back when using the workflow pre-process rename action||Version 1.6 in combination of the Workflow plugin|

Sample HTTP Form 

``` 
<form action="http://demo.razuna.com/index.cfm" name="up" method="post" enctype="multipart/form-data">
<input type="hidden" name="fa" value="c.apiupload">
<input type="hidden" name="api_key" value="54592180-7060-4D4B-BC74-2566F4B2F943">
<input type="hidden" name="destfolderid" value="1">
 
<input type="file" name="filedata">
 
<input type="submit" value="send it">
</form> 
```
Sample CURL command

```
curl -X POST -H "Expect: " -F fa=c.apiupload -F destfolderid=C78950B868CE48168E6DD73CFC8B6519 -F filedata=@myimage.jpg -F api_key=545921807064D4BBC742566F4B2F943 http://demo.razuna.com/index.cfm
```

* Demo Upload Templates :

We have made two examples of uploading assets to Razuna within the API2/demo folder. One example is a simple form post and the other a integration with the popular SWFUpload uploader. You will need to run these two examples from within Razuna in order to work, since they work with Razuna only. 

Flash or Flex :

If you are using a Flash, Flex or AIR application to upload assets to Razuna you will need to use the URL with parameters since Flash only send the filedata id in the post. So you would use the URL of the form action like: [http://demo.razuna.com/index.cfm?fa=c.apiupload&sessiontoken=54592180-7060-4D4B-BC74-2566F4B2F943&destfolderid=1&zip_extract=1](http://demo.razuna.com/index.cfm?fa=c.apiupload&sessiontoken=54592180-7060-4D4B-BC74-2566F4B2F943&destfolderid=1&zip_extract=1)
