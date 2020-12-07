# Write excel file
---
- keywords: [[npm xlsx]], [[patterns]]
- author: [[Alex]]
---
Here is how you write an excel file. 

```
var XLSX = require('xlsx');	
var sheet_data=[];
results.getInvoices.forEach(function(i){
	var row = {
		'date':i.date?i.date.toISOString().substring(0,10):'',
		'location_type':i.location_type,
		'gst_type':i.gst_type,
		'customer_type':i.customer_type,
		'invoice_no':i.remote_id,
		'third_party':i.third_party,
		'buyer_gst_no':i.buyer_gst_no,
		'amount_no_tax':i.amount_no_tax,
		'cgst':i.cgst,
		'sgst':i.sgst,
		'igst':i.igst,
		'amount_including_tax':i.amount_including_tax,
		'gstr3b':i.gstr3b?i.gstr3b.for:'',
		'gstr1':i.gstr1?i.gstr1.for:'',
		'gstr9':i.gstr9?i.gstr9.for:'',
	}
	var checks = _.get(i.details,'checks',{});
	Object.keys(checks).forEach(function(key){
		row['check_'+key]=checks[key].status;
	});
	sheet_data.push(row);
});
var ws = XLSX.utils.json_to_sheet(sheet_data);
var wb = XLSX.utils.book_new();
XLSX.utils.book_append_sheet(wb, ws, 'invoices');

var time = new Date().getTime();
XLSX.writeFile(wb, 'out_'+req.user.id+'_'+time+'.xls');
```