**Single-Sign On Option**

**The Goal**

With the single-sign on option you can have users directly sign in to Razuna without the need to enter the name and password.

___

**The Solution**

Single-Sign On works as such that you call the login method directly and pass in the required arguments, as shown below:

```
http://(yourURL)/index.cfm?fa=c.dologin&name=(name)&pass=(password)&tl=true&pass_hashed=true
```

**Arguments**

|Name|Required||
|----|--------|----|
|yourURL|yes|The URL to the DAM part (Tenant/Host) you want to sign in.|
|name|yes|The users login name (username or email address)|
|password|	yes|The password of the user (see pass_hashed below!)|
|tl|yes|set this to true|
|pass_hashed|no|Set this to true if you hash the password with MD5.We highly recommend that you MD5 hash has the password parameter so that you don't transfer the password in plain text!|

> **Security** : Please use this option only if you are using a encrypted connection (SSL) to your Razuna server. For added security, MD5 hash the password!


