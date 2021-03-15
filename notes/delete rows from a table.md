# Delete rows from a table

```sql
delete from invoice
where 
gstin=23 AND
import_data is null AND
portal_data is null;

```