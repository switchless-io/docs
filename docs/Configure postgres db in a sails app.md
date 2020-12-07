# Configure postgres db in a sails app
---
-Keywords:[[how to]]
- author: [[alex]]
---
Step 1: [[Create a local db with pgAdmin]]

Step 2: Install postgres in sails and set a default datastore  
Install postgres adapter>  
npm install sails-postgresql  
Then, go to config/development.js in your sails app. Configure the datastores object with the relevent values:  


Modify the launch.json with the right DB_HOST, DB_USER, DB_PASSWORD and DB_DATABASE values. Refer this doc for more info:  
https://public.3.basecamp.com/p/g8ASWxY1rZxBXarJgwNdkiK2  


Done.

