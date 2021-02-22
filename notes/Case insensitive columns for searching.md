# Case insensitive columns for searching

For every database that use,
```
CREATE EXTENSION citext;
```

Then using table plus find the column that you want to make case insensitive: 
and then make it insensitive
change it from `text` to `citext`


ref: 
- https://stackoverflow.com/questions/15981197/postgresql-error-type-citext-does-not-exist
- https://sailsjs.com/documentation/concepts/models-and-orm/query-language
- https://www.postgresql.org/docs/9.1/citext.html
- https://github.com/balderdashy/sails/issues/4329