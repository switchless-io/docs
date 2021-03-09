---
author:#alex
---
# != also avoids null elements

```sql
select * from invoice
where gstin=24 
and type='expense'
and status !='claimed';
```

You are expecting invoices which does not have status not equal to `claimed`. The output however is invoices whose status `is not null` and not equal to `claimed`. 

If you are intending to run such query, make sure the field is not `null`

## same issue in waterline as well
```javascript
var filter={ // invoices that should have been included in this month
	type:'expense',
	gstin:results.getFiling.gstin.id,
	gst_type:'regular',
	location_type:['interstate','intrastate'],
	customer_type:'b2b',
	status:{
		'!=':'void',
	},
	date:{
		'>=':start_date.toISOString(),
		'<':end_date.toISOString(),
	}

};
Invoice.find(filter).sort('date ASC').exec(callback);
```

Here also - rows with status = `null` is not returned. 