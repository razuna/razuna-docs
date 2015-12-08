**Advanced Topics**

> **Subversion no longer supported** : As of december 2011 we have moved to our code repository to GIT. Please see the GIT pages.

**Installing and Updating Razuna with GIT Access**

How to download the current development version and the latest stable releases of Razuna from the Razuna GIT repository

**Installing and Updating Razuna with Subversion Access (deprecated)**

How to download the current development version and the latest stable releases of Razuna from the Razuna subversion repository

___

**Razuna Cache Configuration**

As of Razuna 1.5, we introduced different caching options. Caching can make a huge performance difference to your application by reducing the overhead associated with producing repeated blocks of functionality. Using a cache inside of Razuna is extremely easy, allowing you a wide variety of ways to not only access the cache, but how you manage and store this cache using both memory, disk, Memcached, MongoDB and CouchBase.

> **Default Cache** : By default, Razuna uses caching already within the "Memory" and "Disk" configuration. You only need to change this if you want to use another caching mechanism like Memcached, MongoDB or CouchBase! 

**Configure Cache**

Changed the default cache configuration is fairly simply. All you need to do is to edit the file "Server.cfc" (located in the WEB-INF folder). Within that file use one of the below configuration options (they should already be in there commented).

**Memcached/CouchBase**

This cache uses a remote memcached (or CouchBase) server as its storage mechanism. The size of this cache is controlled by the server, with items being auto-aged to make room for new items.

```
<cfset cacheregionnew(
    region="razcache",
    props=
        {
        type : 'memcached',
        server : '127.0.0.1:11211',
        waittimeseconds : 5
        }
)>
``` 

**server** is the list of one or more memcached servers that the cache will connect to. 

**waittimeseconds** is the time that Razuna will wait for before cancelling the operation to the server.

If all the servers go away, then the system will operate as normal, except the cache will simply return nothing.

___

**MongoDB**

Using a MongoDB as a caching server is an effective use of this powerful remote document store. Razuna utilises the MongoDB architecture as efficiently as possible, ensuring the minimum overhead is placed in the cache management.

```
<cfset cacheregionnew(
    region="razcache",
    props=
        {
    type : 'mongo',
    server : '10.0.0.1:27017 10.0.0.2:27017',
    db : 'razcache',
    collection : 'nameofregion',
    user : 'username',
    password : 'password'
    }
)>
```

**server** is the list of MongoDB servers that will be used. This is designed to utilise replica shards.

**db** is the name of the database, which defaults to 'razcache'.

**collection** is the name of the collection to use, which defaults to the name of the cache region when created. 

**user** if the remote MongoDB is protected by a username/password, this is the username. 

**password** password if protected

> You need to restart the Razuna server in order to apply the change!

___

**Razuna GIT access**

As of December 2011 GIT is the preferred versioning system and should be used instead of Subversion.

This development code can only be accessed via GIT. In this article, we'll cover the basics of connecting to the Razuna GIT repository. This article assumes that you have GIT already installed and it only covers the most basic commands.

**The Razuna GIT Repository Architecture**

The basic idea of GIT is that the source code and revisions are kept in a repository on a server. Users connect to the repository by using a client program, which allows the user to check out, view, edit, patch, and commit changes to the source code files (only people with given permissions can commit changes).

The Razuna GIT repository is at [http://github.com/razuna/razuna](http://github.com/razuna/razuna.git). We follow the Git-Flow architecture and thus the repository is setup in sections:

   * develop: contains the latest development code (this might break your code - do NOT use in production)
   * master: Always contains the latest released code
   * release branches: Contains single code fragments with added features (will eventually be merged into develop and removed)

Furthermore, you can download the released code within the "TAGS".

**Checking out of the Razuna code**

Once you have GIT installed, the first step you'll need to do is to check out the code, which basically means that you will download a version from the repository to your computer. To do this, navigate to the directory you want to checkout Razuna and issue the following command:

```
git clone http://github.com/razuna/razuna.git
```

The result will be that the directory is filled with all of the needed Razuna files. The clone will include the latest development branch (master), any other development branches and all official releases (as tags).

**Updating to the latest Razuna code**

If you would like to update to the latest version now available, use the "pull" command, after first changing to the directory where you checked out the code originally:

```
git pull
```

> **Update Tenants** : Additionally to pulling the latest code from GIT you will need to update your tenants/hosts. Please see [Activate hosts with new settings](http://wiki.razuna.com/display/ecp/Activate+hosts+with+new+settings)

> After each pull you need to hit your Administration at [http://localhost:8080/razuna/admin](http://localhost:8080/razuna/admin) as we might have done some updates and the update script needs to run!



