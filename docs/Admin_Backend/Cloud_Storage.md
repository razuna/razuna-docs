**Cloud Storage**

Razuna comes with a cloud storage option. Enabling any of the cloud storage providers will store all of your files with the chosen cloud storage provider and **not** on your local file system anymore.

> **Your files** : If you switch the storage settings on a production system with files already in the system you need to re-add all your files. Under some circumstances the Razuna team can provide a script or further help on moving your files to a cloud storage provider. Please contact us directly!

___

**Akamai**

With the Akamai cloud storage selected all your files will be stored on the Akamai NetStorage. In order to activate Akamai simply select the Akamai option from the cloud storage provider list and additionally enter the Security Token (give to you by Akamai).

![](/Admin_Backend/img/Akamai_1.png)

Once done, you have to configure the URL and paths for each file type in the Tenant Settings.

![](/Admin_Backend/img/Akamai_2.png)

Make sure to enter the full URL for the Akamai endpoint. Also, enter the dedicated path for each file type, e.g. for images "/images/", etc.

> **Akamai Configuration** : The Akamai integration needs a Akamai Configuration on Akamai's end that has to be pushed to your Akamai server. Please contact your Akamai representative and tell them that you use Razuna!

___

**Amazon Web Services (AWS) or Eucalyptus**

 In order to activate AWS or Eucalyptus cloud storage simply select the option from the cloud storage provider list and additionally enter the relevant Security Tokens provided to you by the cloud storage provider.

![](/Admin_Backend/img/AWS_Eucalyptus-1.jpg)

Once done, you have to configure the bucket in the Tenant Settings and you are done. All assets will now be stored in designated bucket for the tenant.

![](/Admin_Backend/img/AWS_Tenant_Setting.jpg)



