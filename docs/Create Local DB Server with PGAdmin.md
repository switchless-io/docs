## Create Local DB Server with PGAdmin  
Keywords:[[how to]]

1. Install postgres. Make sure this is running whenever you want to use the db.  
2. Install pgadmin - https://www.pgadmin.org/download/  
3. If you open postgres, you can see that there's a server created already.  

![](/files/Pasted image 2.png)
Note that, under the server you can see existing databases.  

5. How to create a new database:  
In pgAdmin, right click on the local server to get the option.   

![](Pasted image 3.png)
6. Set a name and choose and owner  
![](Pasted image 4.png)

7. By default, you have one set of credentials to access this db - the owner's credentials  

8. Connect to the db using TablePlus:  
![](Pasted image 5.png)
9. How to create new logins for db:  
![](Pasted image 6.png)
Set name, password, privileges, etc  
![](Pasted image 7.png)
Use the new username and password to connect to db.  
