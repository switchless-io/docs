# List page Filters
---
- keywords: #pattern,
- author: #alex
---
![[Pasted image 20201111163643.png]]

![[Pasted image 20201111163656.png]]
![[Pasted image 20201111163726.png]]

This is implemented as a section on the left side on a laptop screen. 

## Features
### Micro interactions on button click

Sample code
```
<div class='ui grid'>
	<div class='four wide column'>
		<form class="ui form segment" action="" method='get'>
					
			<div class="field">
				<label>Account:</label>
				<div class="ui fluid filter_txn scrolling dropdown basic button">
					<input type="hidden" name="gstin" value='<%=req.query.gstin?req.query.gstin:''%>'>
					<i class="dropdown icon"></i>
					<div class="text">All</div>
					<div class="menu transition hidden" tabindex="-1">
						<!-- <div class="item active selected" data-value='all'>All</div> -->
						<%gstins.forEach(function(a){%>
							<div class="item" data-value='<%=a.value %>'><%=a.value%> - <%= a.business_name%></div>
						<%})%>
					</div>
				</div>
			</div>
			<div class="ui buttons">
			<div class='ui orange left aligned button' id='submit_form'>Apply filter</div>
			<div class='ui blue right aligned button' id='reset_form'>Reset</div>
			</div>
		</form>
	</div>
	<div class='twelve wide column'>
		
	</div>
</div>
```

```
// set up the form
$('.ui.form').form({
	fields: {
	},
	onSuccess:function(e,fields){
		$(this).addClass('loading');
	},
});

$('#submit_form').click(function(){
	console.log('clicked on form submit');
	$('input').each(function(i) {
		var $input = $(this);
		if ($input.val() == '')
			$input.attr('disabled', 'disabled');
	});
	$( "form" ).submit();
});
$('#reset_form').click(function(){
	window.location = window.location.pathname;
	$(this).addClass('loading');
});
```