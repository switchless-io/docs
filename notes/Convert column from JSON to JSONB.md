# Convert column from JSON to JSONB
---
- author: #alex 
---

```sql
ALTER TABLE list
 ALTER COLUMN details
 SET DATA TYPE jsonb
 USING details::jsonb;
 ```