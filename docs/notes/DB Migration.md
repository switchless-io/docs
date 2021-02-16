# DB migration

In order to migrate data safely, write migration scripts. [[Scripting with sails]]

## Overall logic for fault free migration
- Script 1 - Write the data in the table to file. 
- Script 2 - Read data from file one by one and update database. 



Fix and rerun .. Clean

Advantages
- one way function - run any number of times and get the same result
- pause and run
- Start run from in between
- run for specific data sets without meddling with code