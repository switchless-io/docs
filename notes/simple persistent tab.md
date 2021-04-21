# Simple persistent tab

Most of the templating is similar to [[simple tab]]. In order to make a tab persistent.

```
<div class='mobile-slider'>
	<div class="ui tabular menu">
		<a class="<%=tab=='raw_email'?'active':''%> item" data-tab="raw_email">Raw Email</a>
		<a class="<%=tab=='extracted_data'?'active':''%> item" data-tab="extracted_data">Extracted Data</a>
		<a class="<%=tab=='transaction'?'active':''%> item" data-tab="transaction">Transaction</a>
		<a class="<%=tab=='simple'?'active':''%> disabled item" data-tab="simple">Attachments</a>
		<a class="<%=tab=='pro'?'active':''%> disabled item" data-tab="pro">Admin</a>
	</div>
</div>
<div class="ui <%=tab=='raw_email'?'active':''%> tab " data-tab="raw_email">  
	<div class='ui grid'>
		<div class='ten wide column'>
			<div class='ui basic segment'>
				<h3>Subject: <%=_.get(pe,'raw.subject')%></h3>
				<%-_.get(pe,"raw['body-html']")%>				
			</div>
		</div>
	</div>
</div>
<div class="ui <%=tab=='extracted_data'?'active':''%> tab " data-tab="extracted_data">
	<div class='content'><pre><%=JSON.stringify(pe.data,null,'  ')%></pre></div>
</div>
<div class="ui <%=tab=='transaction'?'active':''%> tab " data-tab="transaction">
	<div class='content'>
		<pre><%=JSON.stringify(pe.transaction_event,null,'  ')%></pre>
	</div>
</div>
<div class="ui <%=tab=='simple'?'active':''%> tab" data-tab="simple">
	simple
</div>
<div class="ui <%=tab=='pro'?'active':''%> tab" data-tab="pro">
	pro
</div>
```

## set default active tab
Every `tab header` and `tab body` class should have `<%=tab=='transaction'?'active':''%>`

## Tab initialization becomes 
```
$('.tabular.menu .item').tab({
	onLoad:function(t){
		console.log(t);
		var base_url='/org/<%=req.org.id%>/parsed_email/<%=req.params.pe_id%>'
		history.replaceState(t, t, base_url+'/'+t);
	}
});
```