# Confirm
keywords: [[ui pattern]]

```

var r = confirm("Delete this permanently ?");
if (r == true) {
	$.post("/bull/delete", {job_id: job_id}, function(result,status){
		console.log('result = '+result);
		console.log('status = '+status);// this runs only on sucess
		if(status=='success'){
			$(button).removeClass('loading');
			$(button).addClass('disabled');
		}
	});
} else {
	$(button).removeClass('loading');
}
			
```