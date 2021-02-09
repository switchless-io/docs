# Upload files drop zone UI

## About: 
Normally it looks like this. 
![[Pasted image 20210209182309.png]]

When we drag a file over it, it will look like this: 
![[CleanShot 2021-02-09 at 21.30.11@2x.png]]

## HTML code 

```html
<style type="text/css">
	#uploader {
		border: 4px dashed orange;
	}
	#uploader.hover {
		border-color: black;
		color: black;
	}
</style>
<div class='ui container'>
	<form class="ui form" id='file_upload_form' action="" method='post' enctype="multipart/form-data">
		<%if(1){%>
			<input hidden type="file" id="file_upload" name="files" multiple>
		<%}else{%>
			<input type="file" id="file_upload" name="files" multiple>
			<button class='ui button file_upload'>Submit</button>
		<%}%>
	</form>
	<div class='ui center aligned segment' id='uploader'>
		<br>
		<br>
		<br>
		<br>
		<h1><i class="upload icon"></i> Drop files here to upload</h1>
		<br>
		<br>
		<br>
		<br>
	</div>
</div>
<script type="text/javascript">
	$(document).ready(function(){
		// START - file upload
		var counter=0;
		var uploader = $('#uploader');
		var html='';
		uploader.on('drop', function(e){
			e.preventDefault();
			console.log('dropped');
			$(this).removeClass('hover');
			console.log(e.originalEvent.dataTransfer.files.length);
			console.log(e.originalEvent.dataTransfer.files);
			// $('#file_upload').files=e.originalEvent.dataTransfer.files;
			// adding things to the input field 
			document.querySelector('#file_upload').files = e.originalEvent.dataTransfer.files;
			for(var i=0;i<e.originalEvent.dataTransfer.files.length;i++){
				var file = e.originalEvent.dataTransfer.files[i];
				console.log('\n\n--------');
				console.log(file.name);
				console.log(file.type);
				console.log('--------');
			}
			// submitting the form
			document.getElementById("file_upload_form").submit();
			$('#uploader').addClass('loading');
			$('#uploader').addClass('disabled');
		});
		uploader.on('dragover', function(e){
			e.stopPropagation();
			e.preventDefault();
			$(this).addClass('hover');
		});
		uploader.on('dragleave', function(e){
			e.preventDefault();
			$(this).removeClass('hover');
		});
		// END - file upload

	})
</script>
```