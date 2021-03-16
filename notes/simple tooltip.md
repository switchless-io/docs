# Simple tooltip

## Usage

### Example
```html
<button class='ui teal button' id='sync_portal_data' data-content='Compare invoices in filing portal data with invoices in tracker. Create missing invoices. Update existing invoices. Only import_data is updated. Rest invoice values are unaffected.'>
	Sync Portal Data
</button>
```

### Trigger
```
$("[data-content]").popup({variation:'wide'});
```

### Preferences
```
data-content='content of the popup'
data-position='top left'
```

## Variation

### with help icon
![[Pasted image 20210316114755.png]]
```html
<div data-tooltip="Total taxable value in your income invoices(not including tax)" data-position="top left"> 
	Income <i class="question circle outline icon"></i>
</div>
```

### on button
![[Pasted image 20210316114810.png]]

```html
<button class='ui teal button' id='sync_portal_data' data-content='Compare invoices in filing portal data with invoices in tracker. Create missing invoices. Update existing invoices. Only import_data is updated. Rest invoice values are unaffected.'>
	Sync Portal Data
</button>
```

