### LDAP Server Details

Please enter the details to connect to the LDAP/AD server and search the directory for users that can be imported into the system.
Once setup please go to 'Users>Import>Import LDAP Users' under Administration to manually import the desired users into the system.
Once imported they will be able to log into the system using their LDAP/AD accounts.

![](img/Admin_LDAP_Services.png)

To test that the server is setup properly go to Administration>Users>Import>Import LDAP Users and if you see a list of users populate then the connection was successful. If connection fails then you will see a failure message on that screen.

![](img/admin_LDAP_server_user_list.png) 

If connection is successful you will see a list of users that can be imported into Razuna. Only users with valid emails can be imported. The status column depicts whether user has been imported into the system or not. You can select all available users for import or specific users. You can also specify which groups the user should be assigned to in Razuna.

![](img/admin_ldap_connsuccess.png)

___

**Setting Up Windows AD Server**

To setup a Windows Active Directory server make sure the server type is selected as 'Windows AD' and enter the domain that the AD resides in. The domain is used during authentication and appended to the username e.g. domain\username.

___

**Setting Up LDAP Server**

To setup a LDAP server make sure the server type is selected as 'LDAP' and enter a sample LDAP User Distinguished Name e.g. UID={username},OU=people,DC=razuna,DC=com. The {username} parameter will be replaced with the actual username of the user during authentication.

___

**Common Connection Issues**

**Authentication Exception:** Please verify that the username and/or password credentials to connect to the server are entered correctly.

**Size Limit Exceeded Exception:** Razuna does not support paging while retrieving users so if the number of users are above limit you will see this exception. In this case please specify a filter in the 'Filter' attribute on the LDAP/AD setup screen to trim down the result set e.g. (&(objectClass=user)(samAccountName=a*)) to only retrieve all users whose usernames begin with 'a'. This will bypass the error and once the 'Import LDAP Users' screen loads up you can use the 'Filter' search bar to dynamically filter and retrieve the users from the LDAP/AD server.

**Name Not Found Exception:** Please ensure that the user details and 'Start' DN attribute is specified properly.

**Time Out Exception:** The server could not be contacted after several tries. Please check that the server name or IP is entered correctly and that it is accessible. If server is behind a firewall than it will need to be opened to allow a connection to be formed to the Razuna server. The Razuna hosted server IP is 176.9.139.69. 