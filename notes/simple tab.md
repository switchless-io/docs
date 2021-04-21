---
author: #alex 
---
# simple tab


```
<div class='ui container'>
	<div class="ui tabular menu">
		<a class="item" data-tab="first">First</a>
		<a class="item" data-tab="second">Second</a>
		<a class="item" data-tab="third">Third</a>
		<a class="item" data-tab="simple">Simple</a>
		<a class="item" data-tab="pro">Pro</a>
	</div>
	<div class="ui tab " data-tab="first">	
		First
	</div>
	<div class="ui  tab " data-tab="second">
		Second
	</div>
	<div class="ui tab " data-tab="third">
		Third
	</div>
	<div class="ui tab" data-tab="simple">
	    simple
	</div>
	<div class="ui tab" data-tab="pro">
	    pro
	</div>
</div>
```

```
$('.tabular.menu .item').tab();
```
