

# Creating a copy of the production database in your local host
keywords: [[postgresql]], [[how to]]

**[Loom video](https://www.loom.com/share/84c95cc6243a4ea084957b8ce47c4648)**   
<div style="position: relative; padding-bottom: 62.5%; height: 0;"><iframe src="https://www.loom.com/embed/84c95cc6243a4ea084957b8ce47c4648" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe></div>

**1) Take backup using table plus**

- Pg version 12.0
- Options - none. Remove all options

**2) Clean up the file**

The dump file will contain permission grants to database users created on production db. 

If you dont have those db users on your local postgres server, you need to cleam up the file 

- Once you get the file, open the file 
- Search for rdsadmin and metabase
- Comment out these lines containing rdsadmin or metabase

**3) Drop the db locally**

You can do this using tableplus or with terminal 
```
sudo -u alex.jv dropdb sanitiser_test
```

**4) Create the database locally**

Again you can do this via table plus or via terminal

Create database mralbert_test

```
sudo -u alex.jv createdb mralbert_test -O rdsuser
```

- change `alex.jv` to your mac username
- change `mralbert_test` to the name of your database

**5) Restore database**
```
psql mralbert_test < mralbert.dump
```

- change `mralbert_test` to the name of your database
- change `mralbert.dump` to the name of the dump file
