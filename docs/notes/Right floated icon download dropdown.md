# Right floated download dropdown
---
- keywords: [[ui pattern]]
- author: #alex
---
![[CleanShot 2020-11-28 at 17.02.57.png]]
```
<div class="ui right floated basic icon dropdown button">
	<i class="download icon"></i>
	<div class="menu">
		<div class="header">
			<!-- <i class="download icon"></i> -->
			Download as : 
		</div>
		<div class="item download_as" data-download-as="csv">
			CSV
		</div>
		<div class="item download_as" data-download-as="xls">
			XLS
		</div>
		<div class="item download_as" data-download-as="json">
			JSON
		</div>
	</div>
</div>

```


in document.ready
```
$('.dropdown').dropdown();
$('.download_as').click(function(e){
	e.preventDefault();
	console.log('hi');
	var download_as = $(this).attr('data-download-as');
	console.log(download_as);
	$('input[name=download_as]').val(download_as);
	//download using the form as we want the filters to apply to the download as well. 
	$( "form" ).submit();
	// form by default adds a loading class. that is not required here. 
	$('form.loading').removeClass('loading');
	// clearing the value so that the filter form can be further used. 
	$('input[name=download_as]').val('');
});

```


Add field to form
```
<div class="hidden field">
	<label>Download as:</label>
	<input type='text' name="download_as" value=''>
</div>

```