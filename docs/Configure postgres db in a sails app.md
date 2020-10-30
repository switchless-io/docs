# Configure postgres db in a sails app
Keywords:[[how to]]

Step 1: [Create a local db with pgAdmin](Create%20Local%20DB%20Server%20with%20PGAdmin)  

Step 2: Install postgres in sails and set a default datastore  
Install postgres adapter>  
npm install sails-postgresql  
Then, go to config/development.js in your sails app. Configure the datastores object with the relevent values:  


Modify the launch.json with the right DB_HOST, DB_USER, DB_PASSWORD and DB_DATABASE values. Refer this doc for more info:  
https://public.3.basecamp.com/p/g8ASWxY1rZxBXarJgwNdkiK2  


Done.

