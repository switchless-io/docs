---
author: #alex 
---
# Form success/error message

```html
<form class="ui <%-success?'success':''%> form" id='file_upload_form' action="" method='post' enctype="multipart/form-data">
	<div class="ui success message">
		<div class="header">Files uploaded! - the following files are uploaded: </div>
		<ul class="list">
			<%uploaded_files.forEach(function(filename){%>
				<li><%=filename%></li>
			<%})%>
		</ul>
		<br>
		Track the processing of the files from the <a href="/bull/queue">bull queue</a>
	</div>
	... rest of the form comes here .. 
	
</form>


```