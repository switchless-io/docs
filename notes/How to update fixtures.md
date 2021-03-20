---
author: #alex 
---
# How to update fixtures


## Step 1 :  Using table plus - Take backup
-   Pg version 12.0
-   Options - none. Remove all options
-   Once you get the file, open the file
-   Search for rdsadmin
-   Comment out these lines containing rdsadmin
-   Drop the db locally

## Step 2 : Using terminal - Load fixture 
### Drop db
`sudo -u alex dropdb sanitiser_test`

### Create db
`sudo -u alex createdb sanitiser_test -O rdsuser`

### Restore database  
`psql highlyreco_test < highlyreco.dump`

### Eg code for for Mr Albert

```bash
sudo -u alex dropdb mralbert_test
sudo -u alex createdb mralbert_test -O rdsuser
# got mralbert.dump from step 1  
psql mralbert_test < /Users/alex/Downloads/mralbert.dump 
```


## Other reference 

### Convert .dump to sql
`pg_restore mydb_backup.dump > sql_statements.sql`
### download directly
`psql -h cashflowy.us-east-1.rds.amazonaws.com -U rdsuser mralbert_dev < mralbert.dump`


`psql -h asyncauto.us-east-1.rds.amazonaws.com -p 5432 -d highlyreco\_test -U rdsuser -W -f /Users/alex/Documents/highlyreco\_again.dump`