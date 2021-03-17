# Default toast
This is the preferred toast step.

## Examples 
### success
![[Pasted image 20210316135419.png]]

```
showToast({
	class:'success',
	title: 'Job added to queue',
	message: 'A job for syncing portal data is added to the queue. This will create individual jobs for every invoice that has to be synced',
})
```

### Error
![[Pasted image 20210316135704.png]]
```
showToast({
	class:'error',
	title: '500 error',
	message: 'Error on the server.',
})
```

### Warning
![[Pasted image 20210316135856.png]]
```
showToast({
	class:'warning',
	title: 'You dont have access',
	message: 'You dont have necessary permission to the endpoint that you are trying to access',
})
```

### Info
![[Pasted image 20210316135958.png]]
```
showToast({
	class:'info',
	title: 'You have a new message',
	message: 'Alex send you a new message',
})
```
## Implementation

### Wrapper
```
var showToast=function(options){
	$('body').toast({
		class:options.class,
		title: options.title,
		showProgress: 'top',
		message: options.message,
		className: {
			toast: 'ui message'
		}
	});
}
```

Define this in your layout file. Make sure this is outside document.ready but within the script tag. 