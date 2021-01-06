# Right floated button
---
- keyword: [[ui pattern]], [[button]]
- author: #alex
---

![[CleanShot 2020-11-27 at 11.53.42.png]]

The right floated button is something that is useful to show on top of a table on the right side. 


Just add the class `right floated` and you are good to go. 
```
<button class='basic green ui right floated button' id='rerun_all_checks'>
	Rerun all checks
</button>
```


## Align with something specific
Incase you want to align with something specific, include the button in the tag that you want to align with. 
```
<h3>
	Income invoices
	<a class='ui basic green button right floated' href="/gstin/<%=req.gstin.value%>/invoice/create?type=income">Create income invoice</a>
</h3>
```

![[CleanShot 2020-11-27 at 11.56.14.png]]