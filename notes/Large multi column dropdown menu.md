# Large multi-column dropdown menu

---
- Author: #anzal 

---

## Appearance
![[Pasted image 20210218110645.png]]
## Implementation

**Trigger button**
```html
<div class="ui text menu">

<div class="admin_menu item">

<i class="sidebar icon"></i>

</div>

</div>
```



**Custom Menu with grids**

- create a popup and add it below the menu
- set `inset` in *style* of the popup to position it where you want
```html
<div class="ui flowing basic admission popup bottom left transition" 
style="inset: 3em auto auto 42px;">

	<div class="ui three column relaxed divided grid">

		<div class="ui row">
			<div class="ui column">
				<h3 class="ui header">Manage Clients</h3>
				<div class='ui list'>
					<a href="" class="org item">List all Organizations</a>
					<a href="" class="client item">List all clients</a>
				</div>
			</div>
			
			<div class="ui column">
			</div>
			
			<div class="ui column">
			</div>
		</div>
	</div>
</div>

```


