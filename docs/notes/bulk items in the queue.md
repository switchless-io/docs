# bulk create items in the queue
---
- author: #alex
---

```javascript
var jobs = [];
chunks.forEach(function(chunk){
	var job={
		name:'crawl',
		data:{
			title:'Crawl data from GST portal - GSTR2A - Audit',
			options:{
				what:'gstr2a',
				mode:'audit',
				gstin:req.params.gst_no,
				run_config:{
					"mralbert_host": "https://app.mralbert.in",
					// "client_slug": "sv_engineering",
					"client": {
						// "slug": "sv_engineering",
						"name": gstin.business_name,
						"username": _.get(gstin.details,'config.portal_username'),
						"password": _.get(gstin.details,'config.portal_password'),
						// "plan_type": "filing",
						"gstin": gstin.value,
						// "first_month": "Feb 2020",
						"dob": _.get(gstin.details,'config.dob'),
						// "gstr1_frequency": "monthly",
						"specific_filings": _.map(chunk,'for')
					}
				}
			}
		}
	}
	jobs.push(job);
});

// assuming that this is called from an async function 
await crawlerQueue.addBulk(jobs);
res.redirect('/admin/gstin/'+req.params.gst_no+'/crawl_gstr2a?success=success');


```



```
for (invoice of results.getAllInvoices){
	console.log(invoice);
}					
```