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

## Read line one by one
use async.eachlimit to speed up delays due to network delays. 

## Debug steps
- verify if you are writing to the correct database. modify the data manually and pull the data to file. that should tell if you are reading from the right file. 
- make sure models are modified
- make sure the db is manually updated
- use fs readline
- use async.eachlimit to send multiple update requests simultaneously to speedup network delays.