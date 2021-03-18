# Server responses

## Bad request
```
res.send(400,'bad request');
```
## Not found
```
res.notFound();
```
## API response
```
res.send(200,'ok');
```
## Error
```
res.serverError(err);
```