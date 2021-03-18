# Simple inline dropdown


## eg
```
<span>		
	Checks depth: 
	<div class="ui inline dropdown">
		<div class="text">
			2
		</div>
		<i class="dropdown icon"></i>
		<div class="menu">
			<div class="item">
				2
			</div>
			<div class="item">
				3
			</div>
		</div>
	</div>
</span>
```

## preferred usage
use it to change a single query parameter 

```
<span>		
	Checks depth: 
	<div class="ui inline dropdown">
		<div class="text">
			<%=req.query.checks_max_depth%>
		</div>
		<i class="dropdown icon"></i>
		<div class="menu">
			<a class="item" href='?checks_max_depth=2'>
				2
			</a>
			<a class="item" href='?checks_max_depth=3'>
				3
			</a>
		</div>
	</div>
</span>
```