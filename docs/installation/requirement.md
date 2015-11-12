# Requirement

Razuna is available and tested on the following platforms:

* RedHat 4.x/5.x and later versions (includes CentOS) (tested up to RedHat 6.5)
* Ubuntu 8.04/8.10 and later versions (server and desktop) (tested up to 14.04 LTS)
* MacOS X 10.x and later versions (server and desktop) (tested up to 10.9.x)
* Windows 2003/2008 R2 (tested up to Windows Server 2012)

Not tested, but known to work are :

* OpenSuse 11
* Any version of Debian Linux
* Solaris/OpenSolaris

**Database Support :**

Razuna comes with a high performance embedded database and runs by default on this database. You can also use Razuna with the [ MySQL database](http://wiki.razuna.com/display/ecp/MySQL) or an [Microsoft's MS SQL server.](http://wiki.razuna.com/display/ecp/MSSQL)
___

# Server Requirement

The recommendation for a server setup greatly depends on the usage. Rule of thumb is to have as much memory (RAM) available to the Razuna server as possible. You can run Razuna with 8GB RAM, but if you look into uploading 10'000 images or large images or videos the server needs to have enough ressources to "work" with the files. Configuring a Java application is unfortunately not a "fixed" thing and should be tuned individually. That said, our recommendation is a server with:

 * 16GB RAM
 * 3Ghz CPU

Storage depends on your deployment. But in any case, fast disk access will benefit the overall performance. 
___
# Client Requirement

**What you should have ready and installed for Razuna to work 100%**

Razuna is a web based Digital Asset Management and in this regard all you will ever want and need for Razuna is a web browser. Apart from that you should have some common plug ins installed (which you most probably already have). Please consult the list below to see that you got the recommended setup correctly.

**Browser :**

Windows:

- Internet Explorer (from version 8.x on)
- FireFox
- Safari
- Google Chrome

MacOS X:

- Safari
- FireFox
- Google Chrome
- Chromium

Linux:

- FireFox
- Google Chrome
___

**Plugins (optional) :** **QuickTime**

The Quicktime player from Apple is being used for all other videos that the Flash Player can not play (WMV and some sort of strangely encoded movies that the Flash Player can not pick up). This means that Windows users will need to install the Quicktime Player from Apple. If you are watching Trailers from Apple's website you most likely have Quicktime already installed, if not you should go to [Apple's Quicktime website and install the plugin now.](http://www.apple.com/quicktime/download/)
MacOS X users should install the Flip4Mac plugin to be able to enjoy a error free WMV playback. Flip4Mac will install certain libraries for the Quicktime player and will make it possible to show WMV movies within the browser. [Flip4Mac comes in different flavors, but you only need to install the free version.](http://dynamic.telestream.net/downloads/download-flip4macwmv.htm)
