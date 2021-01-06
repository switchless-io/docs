# Making a POST request
---
- keywords: [[ui pattern]]
- author: #alex
---

```

// setting the variable as `this` is not avaible in the callback of the `post` request. 
var button = this;
$(button).addClass('loading');

// Get data from DOM
var filing_id=$(this).parents('tr').attr('data-id');
var check_type=$(this).parents('tr').attr('data-check-type');
var data = {filing_id: filing_id,check_type:check_type};

// Make post request
$.post("/admin/rerun_checks",data , function(result,status){
	console.log('result = '+result);
	console.log('status = '+status);// this runs only on sucess
	if(status=='success'){
		$(button).removeClass('loading');
		$(button).addClass('disabled');
	}
});

```