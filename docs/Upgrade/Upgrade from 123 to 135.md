**Upgrade from 1.2.3 to 1.3.5**

> *You can only update from Razuna 1.2.3 to Razuna 1.3.5!*

> *Please read the [Update to 1.3 document](/Upgrade/Upgrade from 123 to 13/), since it contains important notes regarding updating from 1.2.3 to a 1.3.x version!*

___

**Overview**

Razuna 1.3.5 is another big point release and as such brings a set of new features and enhancements. The list below is only a short list of new features we added for 1.3. You can lookup the release notes at the public Issue Tracker at [http://issues.razuna.com](http://issues.razuna.com).

___

**Notable Changes**

 * Audio Support.
 * Wordpress Support (via the Razuna Wordpress Plugin).
 * New Javascript Library (faster performance).
 * Many additions to the Developer API.

___

**Update Procedure**

You should always make a backup or Razuna and especially of your database before attempting any update! That said, this process of updating Razuna is quite simple.

 * Download and unarchive the latest release from [http://razuna.org/download](http://razuna.org/download).
 * Stop the Razuna (or J2EE) server.
 * Copy the folders "admin" and "global" of the new version and drop them into your existing Razuna installation folder.
 * Start the Razuna (or J2EE) server.

___

**Hit the Update Page**

Before logging in to Razuna again, you need to run the Update procedure by going to [http://yourdomain/admin/update.cfm](http://yourdomain/admin/update.cfm) (depending on your installation your URL might contain "razuna" as in [http://yourdomain/razuna/admin/update.cfm](http://yourdomain/razuna/admin/update.cfm)). Wait and let Razuna update itself. At the end you will get notified of further actions (if needed).

___

**Update your hosts**

Log in to the Razuna Administration and navigate to "Settings/List/add Hosts" then apply the update to each host that you have in your list .

Your copy of Razuna is now updated and so are all hosts you have.

