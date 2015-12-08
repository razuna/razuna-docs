**Run the Oracle Database scripts**

For the initial setup of a schema for use with Razuna we made a small script that you need to run BEFORE anything else. The script will ask you for the desired schema you want to use (we recommend "razuna") and will give certain grants to this schema. Also it will setup some stored procedures and a custom lexer for Razuna.

> All actions and database interactions from Razuna will take place in this schema. Razuna will never use any other schema information or mess with your database!

___

**Install the script**

To install the script you should navigate to the "(razunadownloaddirectory)/Installation/Databases/Oracle" folder. At the command line issue "Sqlplus" and sign in with "sys as sysdba" and your password.

Then simply call the script with "@razuna.sql". Follow the prompts on the command line.

After you run the script you can check if there are any errors in the "Razuna.lst" file which is being created on runtime in the same directory as the sql script. you can ignore the first error that the Razuna user does not exist, since the script will create one.
