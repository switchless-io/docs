# Filter by start date/end date
---
- keywords: #pattern, [[form]], [[waterline pattern]]
- author: #alex
--- 
![[CleanShot 2020-11-27 at 10.39.56.png]]
This has be used within a [[form]]. 
```
<div class='ui two fields'>
	<div class="field">
		<label>Date from:</label>
		<input type="date" placeholder="YYYY-MM-DD"  name="date_from" value="<%= req.query.date_from ? req.query.date_from: ''%>">
	</div>

	<div class="field">
		<label>Date to:</label>
		<input type="date" placeholder="YYYY-MM-DD" name="date_to" value="<%= req.query.date_to ? req.query.date_to: ''%>">
	</div>
</div>
```

Waterline 
```
var date_from = new Date(req.query.date_from);
var date_to = new Date(req.query.date_to);

if(date_from.toString()!='Invalid Date'||date_to.toString()!='Invalid Date')
	filter.date={}
if(date_from.toString()!='Invalid Date')
	filter.date['>=']=date_from.toISOString();
if(date_to.toString()!='Invalid Date'){
	date_to.setDate(date_to.getDate()+1);
	filter.date['<']=date_to.toISOString();
}
```