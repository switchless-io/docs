# Filter with custom query
When a query needs to be custom written, then the entire filter query might need to get custom written. This can make the query and controller very complex to read or maintain. Eg filter transactions page in cashflowy. 

A solution to that is what we have done with list invoices in Mr Albert. 

```javascript
async.auto({
	getInvoicesWithFailedChecks:function(callback){
		var allowed_checks = _.map(sails.checks.invoice,'slug');
		if(allowed_checks.indexOf(req.query.failing_check)>-1){
			var query = `select id from invoice 
				where gstin = $1
				AND checks::jsonb @> '[{"slug":"${req.query.failing_check}","status":false}]'`
			sails.sendNativeQuery(query,[req.gstin.id]).exec(function(err,result){
				filter.id=_.map(result.rows,'id');
				callback(err,result.rows);
			});
		}else{
			callback(null,null);
		}
	},
	getInvoiceCount:['getInvoicesWithFailedChecks',function(results,callback){
		Invoice.count(filter).exec(callback);
	}],
	getInvoices:['getInvoicesWithFailedChecks',function(results,callback){
		Invoice.find(filter)
		.populate('gstr3b')
		.populate('gstr1')
		.populate('gstr2a')
		.populate('gstr9')
		.populate('documents')
		.sort('date DESC')
		.limit(limit)
		.skip(skip)
		.exec(callback);
	}],
},async function(err,results){
	// done
})
```


In this case, an extra function is written that independantly filters via custom query, gets the ids and updates the filter for the rest of the query. 

## This code is inefficient 
Yes, it is inefficient, but is so much more easy to read and maintain. It works well for moderate scale. 