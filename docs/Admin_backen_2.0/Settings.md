**Settings**

**General Configuration**

Here you will find system wide settings. Host specific settings can be found in the Administration of the host itself. Changes will take effect immediately!

![](/Admin_backen_2.0/img/backen_Settings_GC.png)

___

**Tools**

Razuna uses different third party libraries for creating thumbnails, converting images, videos and audio files to different formats, to extract metadata and more. You need to install these third party libraries first and then enter the absolute path to each library.

*In order to apply changes to this section you need to restart the Razuna server.*

![](/Admin_backen_2.0/img/backend_Settings_Tool1.png)

___

**Backup & Restore**

___

**File Types**

Here you are able to add or remove certain file types according to their extensions. Razuna will look into this table to organize what file belongs to which category. Changes here will affect all tenants. If you are adding an extension make sure that ImageMagick or FFMpeg will be able to handle the extension or else you will get errors! Only edit this table if you know what you are doing!

![](/Admin_backen_2.0/img/backen_Settings_FT1.png)

___

**Trusted Servers**

You need to enter the front end servers you trust below. These trusted servers are able to connect to the API server. You only need to enter a trusted server if you have the Razuna front end server on another network/server. You can enter either a IP address or a DNS name. Note: This is NOT used for public API calls!

![](/Admin_backen_2.0/img/backen_Settings_TS.png)

___

**Scheduled Tasks**

Manage all sytem-wide scheduled tasks. To manage scheduled tasks for a particular host visit the scheduled tasks admin section for that host.

![](/Admin_backen_2.0/img/backen_Settings_Task.png)

To add a new task , you just click into "Add Schedule Task" button and a new add form will appear to allow you create it as below :

![](/Admin_backen_2.0/img/backen_Settings_Task_addnew.png)

If you want to update for current task names in the list , you can click into any task name and then you can edit it.

![](/Admin_backen_2.0/img/backen_Settings_Task_edit.png)