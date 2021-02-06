# Blueprint APIs 
Keywords:

Sailjs comes with blueprint APIs. These blueprint APIs help us default CRUD APIs out of the box. Relevant links from Sailsjs documentations: 

- [RESTful blueprint routes](https://sailsjs.com/documentation/concepts/blueprints/blueprint-routes#?restful-blueprint-routes)


**Typical customisation that we apply over blueprint APIS:**

- routes - `/apis/v1`
- pluralise - `users` instead of `user`
- various authentication strategies 
	- JWT user auth
	- basic secret key auth


**Relevant how-tos:**

- [[How to use blueprint APIs]]
- [[How to use postman collection runner to inject data into database]]


## Source code 



## Known issues 
###  update queries sometimes takes a lot of time.
With sockets and pubsub on, blueprint apis take a lot of time. particularly update queries. 

```
delete req._sails.hooks.pubsub;
```
deleted the pubsub webhook in one of the policies

read code in `sails/lib/hooks/blueprint/action/update`



asdfasf