# How to use blueprint APIs
---
- Keywords:
- author: #alex
---
## RESTful blueprint routes
REST blueprints are the automatically generated routes Sails uses to expose a conventional REST API for a model, including `find`, `create`, `update`, and `destroy` actions. The path for RESTful routes is always `/:modelIdentity` or `/:modelIdentity/:id`. These routes use the HTTP "verb" to determine the action to take.

For example, with rest enabled, having a Boat model in your app generates the following routes:

- GET /boat -> find boats matching criteria provided on the query string, using the [find blueprint](https://sailsjs.com/documentation/reference/blueprint-api/find-where).
- GET /boat/:id -> find a single boat with the given unique ID (i.e. primary key) value, using the [findOne blueprint](https://sailsjs.com/documentation/reference/blueprint-api/find-one).
- POST /boat -> create a new boat with the attributes provided in the request body, using the [create blueprint](https://sailsjs.com/documentation/reference/blueprint-api/create).
- PATCH /boat/:id -> update the boat with the given unique ID with the attributes provided in the request body, using the [update blueprint](https://sailsjs.com/documentation/reference/blueprint-api/update).
- DELETE /boat/:id -> destroy the boat with the given unique ID, using the [destroy blueprint](https://sailsjs.com/documentation/reference/blueprint-api/destroy).

If the Boat model has a “to-many” relationship with a Driver model through an attribute called drivers, then the following additional routes would be available:

- PUT /boat/:id/drivers/:fk -> add the driver with the unique ID equal to the :fk value to the drivers collection of the boat with the ID given as :id, using the add blueprint.
- DELETE /boat/:id/drivers/:fk -> remove the driver with the unique ID equal to the :fk value to the drivers collection of the boat with the ID given as :id, using the remove blueprint
- PUT /boat/:id/drivers -> replace the entire drivers collection with the drivers whose unique IDs are contained in an array provided as the body of the request, using the replace blueprint.

Ref: [Sails blueprint routes](https://sailsjs.com/documentation/concepts/blueprints/blueprint-routes#?restful-blueprint-routes)

<div style="position: relative; padding-bottom: 56.25%; height: 0;"><iframe src="https://www.loom.com/embed/08eeb7ed910f47d6abbe277b680ccacd" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe></div>