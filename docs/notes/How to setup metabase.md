# Setup metabase 
---
- keywords: , #setup, [[metabase]]
- author: #alex
--- 
The process for setting up metabase follows our standard method for deploying any open source subsystem. Dockerise it and make sure the ec2 machine is disposable at any given point of time. 

## Instructions to setup 

1. Create an application on elastic beanstalk. Choose docker as the platform.
2. Pull this config code from https://github.com/asyncauto/metabase and upload it to beanstalk
3. Create a postgresql db
4. Create DNS mapping on cloudflare
5. Add the following env variables to eb env
```
MB_DB_DBNAME: "metabase"
MB_DB_HOST: "abc.database.com" 
MB_DB_PASS: "mypassword" 
MB_DB_PORT: 5432 
MB_DB_TYPE: "postgres" 
MB_DB_USER: "rdsuser"
SERVICE: "metabase"
```

## Email config - Metabase smtp setup

In Mailgun create a new smtp user - metabase@mail.cashflowy.in


Fill up that details on metabase
![](files/metabase-smtp-config.png)


Test to see if it works
![](files/metabase-test-email.png)

Also tried the reset password to see if that works
![](files/metabase-reset-pwd-email.png)

