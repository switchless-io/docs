# Waterline filter by date

```
{
	type:'income',
	gstin:results.getFiling.gstin.id,
	date:{
		'>=':start_date.toISOString(),
		'<':end_date.toISOString(),
	}
}
```