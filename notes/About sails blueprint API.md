# About sails blueprint API


Sailjs comes with blueprint APIs. These blueprint APIs help us default CRUD APIs out of the box. Relevant links from Sailsjs documentations: 

- [RESTful blueprint routes](https://sailsjs.com/documentation/concepts/blueprints/blueprint-routes#?restful-blueprint-routes)


**Typical customisation that we apply over blueprint APIS:**

- routes - `/apis/v1`
- pluralise - `users` instead of `user`
- various authentication strategies 
	- JWT user auth
	- basic secret key auth
