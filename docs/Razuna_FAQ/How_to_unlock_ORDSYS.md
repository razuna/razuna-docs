**How to unlock the ORDSYS account**

By default old some accounts are locked and cannot be used within sqlplus. This especially is the case with the ordsys schema. We therefore need to unlock the schema first before we can log in with that schema. Unlocking a account can be done trough the Enterprise Manager. You can access the Enterprise Manager within your browser at [http://localhost:1158/em/](http://localhost:1158/em/).

> There should be a URL shortcut in your Start Menue in Windows called "Oracle Database - Orcl" which will take you to this URL. Also, make sure that the Enterprise Manager Service is running. If not, go into your "Services" and start up the "OracleDBConsoleORCL" service.

 Log in to the Enterprise Manager with "sys" and your password. Make sure, that you connect as "sysdba".

![](/Razuna_FAQ/img/or1.png)

If this is your first time you login in to the Enterprise Manager you will have to agree to the license information. Else you will see the main page of the Enterprise Manager. 

![](/Razuna_FAQ/img/or2.png)

On top you will see the main navigation. Click on the "Administration" link. You will then get to a list of options.

![](/Razuna_FAQ/img/or3.png)

In the "Users & Privileges" click on "Users". You will then see a list of all the users.

![](/Razuna_FAQ/img/or4.png)

Select the radio button of the user "ORDSYS" and click on "Edit" above the user list. In the detail page you then will be able to modify this user.

![](/Razuna_FAQ/img/or5.png)

Change the password to something secure. Change the status to "Unlocked". If done, click on "Apply" to save the changes.

You can now log out of the Enterprise Manager. Again, to save resources we recommend stopping the Enterprise Manager Service.

> Even if you want to keep the password you will need to re-enter here. If you do not change the password and only unlock the user the account will be set to "Expired"!  

