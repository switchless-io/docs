# Send native SQL query with sails
use `sails.sendNativeQuery` function:

```javascript
var query =
	`SELECT
		*
	FROM
		"user"
	WHERE
		is_active = 'true' AND
		is_va = 'true' AND
		id != ${req.params.id} AND
		details ->> 'training_status' = 'trained' AND
		details -> 'daily_ops' ->> 'shift' = '${results.getUser.details}' AND
		(details -> 'cache' ->> 'availability')::float >= '2'
	LIMIT
		4`;

sails.sendNativeQuery(query, function(err, rawResult) {
	if(err) throw err;
	console.log('users -> similar: rawResult');
	console.log(rawResult);
	callback(err, rawResult.rows);
});
```

or

```
var results = await sails.sendNativeQuery(sql, valuesToEscape);
```