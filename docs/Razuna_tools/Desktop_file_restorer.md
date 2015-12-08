**The Desktop File Restorer**

**What is it?**

The Desktop File Restorer is a desktop client application built with Node.js that allows Razuna users to quickly restore their existing assets by dragging the files to unto the application and clicking 'Upload'.

___

**How does it work?**

The Desktop File Restorer POSTs the files it is given from your computer to the Razuna server.  The Razuna server then matches these files against your previously uploaded assets by MD5 hash; any hash matches found (indicating matching asset data) will result in restoring the asset file in Razuna.  All existing meta-data - such as folder, permissions, labels, etc. - will remain unchanged.

A valid API key is required to ensure that only you and people within your organization can restore files to your account.  Steps to obtain your API key can be found in the instructions below.  

> Please note that the Desktop File Restorer will not upload new data to your account.  New assets should continue to be uploaded directly through the Razuna site or API.

___

**Installation and Configuration**

Detailed step by step instructions for installing and configuring the Desktop Restorer Tool can be found here for MacOSX and here for Windows OS.

___

**How to use the application**

Using the application is quite simple.  Just select the files that you would like to restore, drag them onto the dashed rectangle, and click 'Upload Files'.

![](/Razuna_tools/img/image2014.png)

While files are being uploaded progress indicators will show how far along your files are in the upload process.

Once all files in a given batch have been uploaded, you can drag your next set of files into the rectangle and click 'Upload Files' again.

___

**Mac OSX - Installation and Set-up Instructions for the Desktop File Restorer**

* Download the tool

|Operating System	|Download Link|
|---|----|
|Mac OSX|[Desktop File Restorer for Mac OSX](http://s.razuna.com.s3.amazonaws.com/installers/uploader/restore/Razuna-Uploader.zip)|

* Unzip the file and drag the Razuna-Uploader.app file to your Applications folder

* Open the Razuna-Uploader and click on Settings in the upper right hand corner

![](/Razuna_tools/img/image20141.png)

* On the Settings page enter your hosted site's url and your API key

![](/Razuna_tools/img/image20142.png)

**Obtaining your Url**

* Log into your Razuna account

![](/Razuna_tools/img/image20143.png)


* copy the url in the url bar up to the first '/'

   * for example, using the url from the image above we end up with: demo.cloud.razuna.in

* now append 'http://' to the beginning of this value and that will be your url to use for the uploader tool

   * using the same example the url to use would be : http://demo.cloud.razuna.in 

> **Please note** : It is important to ensure that you do not add a '/' to the end of the entered url. The url entered should end with a letter or number.


**Obtaining your API Key**

  * log into Razuna if you have not already done so

  * In the upper right hand corner of the site click on your name to open a drop down menu and choose 'My info'

![](/Razuna_tools/img/image20144.png)


* This will open a pop up with three tabs, click on the 'API Key' tab

![](/Razuna_tools/img/image20145.png)

* Copy your API key in the yellow box and paste it into the API Key field of the Desktop File Restorer

**Click submit**

* After a brief pause you will get feedback indicating successful or failed credential verification

   * if successful, you're done - click on 'Go to Uploader' to begin restoring your files.
   * if authentication failed, recheck your values entered and submit again.

___

**Windows - Installation and Set-up Instructions for the Desktop File Restorer**

* Download and unzip the application's zip file

|Operating System|Download Link|
|----------------|-------------|
|Windows|[Desktop File Restorer for Windows](http://s.razuna.com.s3.amazonaws.com/installers/uploader/restore/RazunaUploader-installer.exe)|

* Double-click the .exe and follow the installation instructions

* Run the Razuna-Uploader and click on Settings in the upper right hand corner

![](/Razuna_tools/img/image20146.png)

* On the Settings page enter your hosted site's url and your API key

![](/Razuna_tools/img/image20147.png)

**Obtaining your Url**

* Log into your Razuna account

![](/Razuna_tools/img/image20148.png)

* copy the url in the url bar up to the first '/'

   * for example, using the url from the image above we end up with: demo.cloud.razuna.in

* now append 'http://' to the beginning of this value and that will be your url to use for the uploader tool

   * using the same example the url to use would be : [http://demo.cloud.razuna.in](http://demo.cloud.razuna.in) 

> **Please note** : It is important to ensure that you do not add a '/' to the end of the entered url. The url entered should end with a letter or number.

**Obtaining your API Key**

  * log into Razuna if you have not already done so

  * In the upper right hand corner of the site click on your name to open a drop down menu and choose 'My info'

![](/Razuna_tools/img/image20149.png)

* This will open a pop up with three tabs, click on the 'API Key' tab

![](/Razuna_tools/img/image201410.png)

* Copy your API key in the yellow box and paste it into the API Key field of the Desktop File Restorer

**Click submit**

* After a brief pause you will get feedback indicating successful or failed credential verification

  * if successful, you're done - click on 'Go to Uploader' to begin restoring your files.
 
  * if authentication failed, recheck your values entered and submit again.




        