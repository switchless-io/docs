# Create a blueprint object with Ajax


### Html

```html
<button class='basic green ui button create_invoice' data-body='<%=JSON.stringify(i)%>'>
	Create <%=i.type%> invoice
</button>
```

### Javascript

```javascript
$('.create_invoice').click(function(){
	var button = this;
	$(button).addClass('loading');
	var parsed_import_data=JSON.parse($(this).attr('data-body'));
	delete parsed_import_data.tracker_invoice;
	console.log(parsed_import_data);
	// console.log('hello');
	// var job_id='';

	var settings = {
		url:"/apis/v1/invoices/",
		data:JSON.stringify(parsed_import_data),
		"method": "POST",
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
		// location.reload(); // incase you want to reload the page
	});
})
```

