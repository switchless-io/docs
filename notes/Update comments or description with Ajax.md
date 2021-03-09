# Update comments or description with Ajax

```html
<span class='comments'><%-i.comments?i.comments:''%></span>
<a class='edit' data-id='<%=i.id%>' href=''>edit</a><br>

<div class='edit_comments' data-id='<%=i.id%>' style='display:none;'>
	<div class="ui fluid input">
		<textarea rows = "5" name = "comments"><%-i.comments?i.comments:''%></textarea><br>
		<!-- <input type="text" name='comments' value='<%-i.comments?i.comments:''%>'> -->
	</div>
	<br>
	<button class="ui teal button submit_edit_desc" data-id='<%=i.id%>' >save</button>
	<button class="ui red button cancel_edit_desc" data-id='<%=i.id%>' >cancel</button>
</div>	
```

```javascript
$('.edit').click(function(e){
	e.preventDefault();
	$(this).hide();
	var i_id=$(this).attr('data-id');
	// console.log('comments edit clicked');
	// console.log(i_id);
	// if(!edit_active)
	$('tr[data-id='+i_id+']').find('span.comments').hide();
	$(this).parent().find('.edit_comments').show();
	// edit_active=true;
});
$('.cancel_edit_desc').click(function(e){
	// console.log('cancel button clicked');
	var i_id=$(this).attr('data-id');
	// edit_active=false;
	$(this).parent().hide();
	$(this).parents('tr[data-id='+i_id+']').find('span.comments').show();
	$(this).parents('tr[data-id='+i_id+']').find('.edit').show();
	// $(this).parents().find('.edit[data-id='+i_id+']').show();
});
$('.submit_edit_desc').click(function(e){
	// console.log('submit button clicked');
	// var i_id=$(this).parents('.tc').attr('data-t-id');
	var i_id=$(this).attr('data-id');
	// console.log(i_id);
	var comments=$('tr[data-id='+i_id+']').find('[name=comments]').val();
	// console.log(comments);
	$('tr[data-id='+i_id+'] span.comments').text(comments);
	$('tr[data-id='+i_id+'] span.comments').show();
	// /api/edit_desc
	var button = this;
	$(button).addClass('loading');
	$(button).addClass('disabled');
	$.post("/gstin/<%=req.gstin.value%>/api/edit_comments", {invoice: i_id,comments:comments}, function(result,status){
		// console.log('result = '+result);
		// console.log('status = '+status);// this runs only on sucess
		if(status=='success'){
			$(button).removeClass('loading');
			$(button).removeClass('disabled');
			$(button).parent().hide();
			$(button).parents().find('.edit[data-id='+i_id+']').show();
		}
	});
});


```