# Popup pattern 1
---
- keywords: [[ui pattern]]
- author:[[Alex]]
---
![[Pasted image 20201127103052.png]]

HTML popups are very useful. We have used that in [[Highlyreco]] and [[Mr Albert]]. 

Sample code the the above popup
```
<%Object.keys(sails.helpers.checks.invoice).forEach(function(key){%>
	<%
	var check = _.get(i.details,'checks['+key+']',{});
	var check_def=sails.helpers.checks.invoice[key].toJSON()
	%>
	<span class='popup' data-html='<div class="header"><%=check_def.friendlyName 	</div><div class="content"><%=check_def.description%><br><br><b>Comments:</b><br><%-check.comments%></div>'>
		<br><i class="<%=check.status?'green check':'red close'%> icon"></i>
		<%=check_def.friendlyName%>
	</span>
<%})%>

```

```
$('.popup').popup();
```