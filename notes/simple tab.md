---
author: #alex 
---
# simple tab


```
<div class="ui tabular menu">
	<div class="item" data-tab="simple">Simple</div>
	<div class="item" data-tab="Pro">Pro</div>
</div>
<div class="ui tab" data-tab="simple">
	simple
</div>
<div class="ui tab" data-tab="pro">
	pro
</div>
```

```
$('.tabular.menu .item').tab();
```
