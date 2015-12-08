**Enable social network login**

> **Available as of Razuna 1.5** : This option was introduced in Razuna 1.5.

**Social Network Login**

As of Razuna 1.5 the ["Engage" Plugin from Janrain](http://janrain.com/products/engage/) has been integrated which allows your users to use their existing social network accounts (Google, Twitter, Facebook, etc.) to login to Razuna. Actually, the Janrain service allows for over 23 different providers to be used. All providers are automatically supported by Razuna and can be used for your users. Please follow the guide below to setup social login for Razuna.

> **Janrain Engage** : You need a Janrain Engage account to be abe to provide your users with a social network login. [Janrain Engage is a external service](http://janrain.com/products/engage/) and only works if you are connected to the Internet. Furthermore, you might have to [get a paying account](http://janrain.com/products/engage/engage-pricing/) with them if you exceed their options or want enhanced features.

___

**Enable Janrain in Razuna**

Once you have setup your Janrain account and configured all your providers (you need to setup your providers within the Janrain account and NOT in Razuna!) you are ready to enable Janrain in Razuna. To do so, simply copy your Janrain API key and activate the use if Janrain and save it in the Razuna Administration under the new "Integration" tab as shown in the screen shot below.

![](/admin/img/janrain-admin.jpg)

You login screen looks like the one below and allows your users to sign in with their social network accounts.

![](/admin/img/janrain-login.jpg)

Now, **before** your users can use the social network login you need to assign their social network credentials to their account in Razuna, also!

___

**Assign social network credentials for users**

Since your Digital Asset Management site is protected you need to assign the social network credentials of your users to their user account so they can leverage the social network login feature. Doing so is very simple as you only need to have their email address that they registered on the social network or their login name (99% of the time this is their eMail address, thought on Twitter it is their Twitter name!).

In order to add the social network accounts for your users click on the "Social Network" tab in the user dialog and add the login credential for each network provider, e.g. Google, Twitter, Facebook, etc.

![](/admin/img/janrain-accounts.jpg)

That's it. There is nothing else for you to do and your users will experience a seamless login experience without the need for a separate account (thought you need to create a Razuna account, which also works, but they might never know that or can use the Razuna account as well).