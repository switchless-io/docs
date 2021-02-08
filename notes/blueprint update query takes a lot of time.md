---
author: #alex 
---
# Blueprint update query takes a lot of time

update queries sometimes takes a lot of time.
With sockets and pubsub on, blueprint apis take a lot of time. particularly update queries. 

```
delete req._sails.hooks.pubsub;
```
deleted the pubsub webhook in one of the policies

read code in `sails/lib/hooks/blueprint/action/update`
