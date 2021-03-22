---
author:#alex
---
# query size of array in json column in postgres


```sql
SELECT jsonb_array_length('["question","solved"]') AS length;
```

Ref: https://stackoverflow.com/a/33908392/1650911

## Example

```
SELECT json_array_length(portal_data_json->'b2ba') as b2ba,* from filing 
where gstin=31 AND 
type='gstr1';
```

![[Pasted image 20210322163631.png]]





