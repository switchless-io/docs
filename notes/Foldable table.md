---
author: #alex 
---
# Foldable table
## Example
![[CleanShot 2021-02-24 at 12.16.09 2.gif]]

```
<table class="ui selectable celled unstackable collapsing table">
	<thead>
		<tr>
			<th>Check Name</th>
			<th>Total</th>
			<th>Passing</th>
			<th>Failing</th>
		</tr>
	</thead>
	<tbody>
		<tr data-name='one' class='parent'>
			<td>Parent one <i class="icon caret left"></i></td>
			<td>1</td>
			<td>2</td>
			<td>3</td>
		</tr>
		<tr data-parent='one' style="display:none;">
			<td><i class='icon'></i>Child One</td>
			<td>11</td>
			<td>22</td>
			<td>33</td>
		</tr>
		<tr data-parent='one' style="display:none;">
			<td><i class='icon'></i>Child One</td>
			<td>11</td>
			<td>22</td>
			<td>33</td>
		</tr>
		<tr data-name='two' class='parent'>
			<td>Parent two <i class="icon caret left"></i></td>
			<td>1</td>
			<td>2</td>
			<td>3</td>
		</tr>
		<tr data-parent='two' style="display:none;">
			<td><i class='icon'></i>Child two</td>
			<td>11</td>
			<td>22</td>
			<td>33</td>
		</tr>
		<tr data-parent='two' style="display:none;">
			<td><i class='icon'></i>Child two</td>
			<td>11</td>
			<td>22</td>
			<td>33</td>
		</tr>
		<tr data-name='three' class='parent'>
			<td>Parent three <i class="icon caret left"></i></td>
			<td>1</td>
			<td>2</td>
			<td>3</td>
		</tr>
		<tr data-parent='three' style="display:none;">
			<td><i class='icon'></i>Child three</td>
			<td>11</td>
			<td>22</td>
			<td>33</td>
		</tr>
		<tr data-parent='three' style="display:none;">
			<td><i class='icon'></i>Child three</td>
			<td>11</td>
			<td>22</td>
			<td>33</td>
		</tr>
	</tbody>
</table>
```

```
$('.parent').click(function(){
	console.log('check name clicked');
	var parent_name=$(this).attr('data-name');
	console.log(parent_name);
	$('[data-parent="'+parent_name+'"]').toggle()
	if($(this).find('.left').length)
		$(this).find('.left').removeClass('left').addClass('down')
	else if($(this).find('.down').length)
		$(this).find('.down').removeClass('down').addClass('left')
})
```