# Fully loaded tabs with its own url
---
- keywords: [[tabs]],[[ui pattern]]
- author: [[Alex]]
---
```
<%
	// on the top of the page
	var tab=req.params.tab?req.params.tab:'summary';
%>
```



```
// on load update url history
$('.secondary.menu .item').tab({
	onLoad:function(t){
		var base_url='/gstin/<%=req.gstin.value%>/filing/<%=req.params.filing_id%>'
		history.replaceState(t, t, base_url+'/'+t);
	}
});

```

```
<div class="ui pointing secondary menu">
	<a class="<%=tab=='summary'?'active':''%> item" data-tab="summary">Summary</a>
	<a class="<%=tab=='tracker'?'active':''%> item" data-tab="tracker">Tracker</a>
	<a class="<%=tab=='portal_data'?'active':''%> item" data-tab="portal_data">Portal data</a>
	<a class="<%=tab=='checks'?'active':''%> item" data-tab="checks">Basic checks</a>
	<%if(req.user.access_flags.is_admin){%>
		<a class="<%=tab=='admin_actions'?'active':''%> item" data-tab="admin_actions">Admin Actions</a>
	<%}%>
</div>
<div class="ui <%=tab=='summary'?'active':''%> tab" data-tab="summary">
	summary
</div>
<div class="ui <%=tab=='tracker'?'active':''%> tab" data-tab="tracker">
	tracker
</div>
<div class="ui <%=tab=='portal_data'?'active':''%> tab" data-tab="portal_data">
	portal_data
</div>
<div class="ui <%=tab=='checks'?'active':''%> tab" data-tab="checks">
	checks
</div>
<div class="ui <%=tab=='admin_actions'?'active':''%> tab" data-tab="admin_actions">
	admin_actions
</div>
```


![[CleanShot 2020-11-25 at 14.13.41.png]]