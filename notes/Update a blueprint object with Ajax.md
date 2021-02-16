# Update a blueprint object with Ajax
---
- author: #alex 
---

### html
```html
<button class='basic green ui button update_invoice_pd' data-invoice-id='<%=related_invoice.id%>' data-portal-data='<%=JSON.stringify(i)%>'>
	Add portal data to invoice
</button>
```


### javascript 
```javascript
$('.update_invoice_pd').click(function(){
	console.log('hi hi');
	var button = this;
	$(button).addClass('loading');
	var portal_data = JSON.parse($(button).attr('data-portal-data'));
	// delete import_data.details;
	var invoice_id= $(button).attr('data-invoice-id');
	// console.log('delete details done');
	// console.log('going to update invoice now');
	console.log(portal_data);
	var data = {
		portal_data:portal_data,
		gstr2a:"<%=req.params.filing_id%>",
	}
	var settings = {
		url:"/apis/v1/invoices/"+invoice_id+'?gstin=<%=req.gstin.value%>',
		data:JSON.stringify(data),
		"method": "PATCH",
		"timeout": 0,
		"headers": {
			"Content-Type": "application/json",
		},
	};
	// console.log(settings);
	$.ajax(settings).done(function (response) {
		// console.log(response);
		$(button).removeClass('loading');
		$(button).addClass('disabled');
		// location.reload(); // incase you want to reload the page after this action
	});
});
```