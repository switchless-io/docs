# Dropdown with header
keywords: [[form]], [[dropdown]], [[ui pattern]]

## How it looks like: 
![[Pasted image 20201103172517.png]]

## Template code

```
<form class='ui form' method='post'>
	<div class="field">
		<label>File type</label>
		<div class="ui fluid search selection dropdown">
			<input type="hidden" name="file_type" placeholder="Choose file type" value="">
			<i class="dropdown icon"></i>
			<div class="default text">Choose file type</div>
			<div class="menu">
				<div class="divider"></div>
				<div class="header"><i class="file icon"></i> GSTR1 related</div>
				<div class='item' data-value="sales"></i>Import sales</div>
				<div class='item' data-value="sales"></i>Import Credit Notes</div>
				<div class="divider"></div>
				<div class="header"><i class="file icon"></i> GSTR2A related</div>
				<div class="item">Import GST input sheet</div>
				<div class="item">Import IGST input</div>
			</div>
		</div>
	</div>
</form>
```

```
<script type="text/javascript">
	$(document).ready(function(){
		$('.dropdown').dropdown();
	})
</script>
```