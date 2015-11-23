**Upgrade from 1.2.2 to 1.2.3**

> **Upgrade from 1.1.4 or 1.2** : *You can upgrade from Razuna 1.1.4 or 1.2 directly to Razuna 1.2.3!*

___

**Overview**

Razuna 1.2.3 contains a couple of new features is also a bug fix release. You can always lookup the release notes and upcoming features of Razuna at the public Issue Tracker at [http://issues.razuna.com](http://issues.razuna.com).

___

**Notable Changes**

* New: Dutch Translation: Thanks to David Wuyts, a Razuna Community Member, we are able to offer you Razuna in Dutch now.
* New: Code Optimization for better performance and upload speed.
* New: API call to retrieve the complete Folder Tree.
* Fix: Moving and creating folders did not allow you to create another one with the same name.
* Fix: Moving images to another folder did sometimes loose the thumbnail and image itself.
* Fix: Batching of Video keywords did not work.
* Fix: The user list shows now the correct username, first and last name entry.

___

**Update Procedure**

You should always make a backup or Razuna and especially of your database before attempting any update! That said, this process of updating Razuna is quite simple.

 * Download and unarchive the latest release.
 * Stop the Razuna (or J2EE) server.
 * Copy the folders "admin" and "global" of the new version and drop them into your existing Razuna installation folder.
 * Start the Razuna (or J2EE) server.

___

**Update your hosts**

Log in to the Razuna Administration and navigate to "Settings/List/add Hosts" then apply the update to each host that you have in your list

Your copy of Razuna is now updated and so are all hosts you have.
