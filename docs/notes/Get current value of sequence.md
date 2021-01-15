# Get current value of sequence 
---
- author: #alex 
- tags: #how_to 
---

## Best way
```sql
SELECT last_value FROM your_sequence_name;
```

## Not recommended
currval is only relevant for the current session. This will only return the last value set in your session. If someone else is generating entry it will not reflect in `currval`
```sql
select currval('names_id_seq');
```
