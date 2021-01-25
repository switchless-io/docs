# filter by a field 




```
if(req.query.third_party && req.query.third_party!='empty'){
	filter.third_party={
		contains:req.query.third_party
	}
}
if(req.query.third_party=='empty'){
	filter.or=[
		{third_party:null},
		{third_party:''},					
	]
}
```

### explanation

First if condition filters the the field by value in query params

Second if condition filters the field by null or empty