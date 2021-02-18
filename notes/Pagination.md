# Pagination
---
- keywords: #pattern
- author: #alex
---
**pagination menu looks like this: **
![[Pasted image 20201102161833.png]]


**url looks like this: **
![[Pasted image 20201102161844.png]]

## EJS code
```
<!-- Add this function to the top of the page -->
<%
	function updateQueryStringParameter(uri, key, value) {
		var re = new RegExp("([?&])" + key + "=.*?(&|$)", "i");
		var separator = uri.indexOf('?') !== -1 ? "&" : "?";
		if (uri.match(re)) {
		  return uri.replace(re, '$1' + key + "=" + value + '$2');
		}
		else {
		  return uri + separator + key + "=" + value;
		}
	}
%>





<!-- Add this to where you want to see your pagination -->
<div class="ui pagination menu">
	<a class="<%= page==1?'disabled':''%> item" href="<%=page==1?'#':updateQueryStringParameter(req.url, 'page', page-1)%>">
		<i class="icon caret left"></i>
	</a>
	<div class="item">
		<%=page%> / <%=pages%> 
	</div>
	<a class="<%= page==pages?'disabled':''%> item" href="<%=page==pages?'#':updateQueryStringParameter(req.url, 'page', page+1)%>">
		<i class="icon caret right"></i>
	</a>
</div>
&nbsp;&nbsp; Showing upto <%=limit%> invoices per page
```

## Variables needed in locals
- page (shows the current page)
- pages (total number of pages)
- limit (number of items per page)


## Template controller for pagination

```
listInvoices:function(req,res){

	var filters = {}
	var limit = req.query.limit?parseInt(req.query.limit): 100;
	var page = req.query.page?parseInt(req.query.page):1;
	var skip = limit * (page-1);


	async.auto({
		getInvoiceCount:function(callback){
			Invoice.count(filters).exec(callback);
		},
		getInvoices:function(callback){
			Invoice.find(filters)
			.sort('createdAt DESC')
			.limit(limit)
			.skip(skip)
			.exec(callback);
		}
	},function(err,results){

		if(err)
			throw err;
		var locals={
			page:page,
			limit:limit,
			pages: Math.ceil(parseFloat(results.getInvoiceCount/limit)? parseFloat(results.getInvoiceCount/limit) : 1),
			invoices:results.getInvoices,
		};
		res.view('list_invoices',locals);
	})
}

```


