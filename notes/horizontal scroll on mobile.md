# Horizontal scroll on mobile
This is useful on mobile 

```
 <style>
  .hidden {
	display: none !important;
  }
  html{
	overflow-y: scroll;
	overflow-x: hidden;
  }
  .mobile-slider {
	min-width: 100%;
	display: flex;
	overflow-x: auto;
  }
  .mobile-slider::-webkit-scrollbar {
	display: none;
  }
</style>
```

```html
<div class='mobile-slider'>
	<div class="ui tabular menu">
		<a class="item" href='/gstin/<%=req.gstin.value%>'>Overview</a>
		<a class="item" href='/gstin/<%=req.gstin.value%>/filings'>Filings</a>
		<a class="item" href='/gstin/<%=req.gstin.value%>/invoices'>Invoices</a>
		<a class="item" href='/gstin/<%=req.gstin.value%>/activities'>Activity</a>
		<a class="item" href='/gstin/<%=req.gstin.value%>/tasks'>Tasks</a>
		<a class="item" href='/gstin/<%=req.gstin.value%>/documents'>Docs</a>
		<a class="item" href='/gstin/<%=req.gstin.value%>/third_parties'>3rd parties</a>
		<a class="item" href='/gstin/<%=req.gstin.value%>/reports'>Reports</a>
		<%if(req.user.access.type!='auditor'){%>
		<a class="item" href='/gstin/<%=req.gstin.value%>/settings'>Settings</a>
		<%}%>
		<%if(req.user && _.includes(sails.config.admins, req.user.email)){%>
			<%if(req.user&&req.user.id==1){%>
			<a class="item" href='/gstin/<%=req.gstin.value%>/import'>Import</a>
			<%}%>
		<a class="item" href='/gstin/<%=req.gstin.value%>/admin'>Admin</a>
		<%}%>
	</div>
	<br>
</div>
```



![[CleanShot 2021-02-20 at 20.17.37.gif]]