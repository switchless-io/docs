# Find duplicate elements 

```
select gstin,count(*),remote_id,"type" from invoice
group by gstin, remote_id,"type"
HAVING count(*) > 1
order by count desc;
```


