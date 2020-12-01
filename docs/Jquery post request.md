# Jquery post request
keywords: [[jquery]], [[ui pattern]]

```
$.post("/gstin/<%=req.gstin.value%>/import/create_invoice/expense", body, function(result,status){
	console.log('status = '+status);// this runs only on sucess
	console.log('result = '+result);
	// if(status=='success'){
	$(button).removeClass('loading');
	$(button).addClass('disabled');
	// }
}).fail(function(result,status){

	console.log('status = '+status);// this runs only on sucess
	console.log('result = '+JSON.stringify(result,2,2));
	$(button).removeClass('loading');
	$(button).addClass('disabled');
	$(button).text('Error');
});

```