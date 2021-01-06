# Click button on the screen in bulk
---
- keywords: [[ui]],#pattern
- author: #alex
---
```
$('#create_all_invoices').click(function(){
	$(this).addClass('disabled');
	var buttons = $('.create_invoice:not(.disabled)');
	buttons.each(function(i){
		setTimeout(function(){ 
			$(buttons[i]).click()
			// console.log(i) 
		}, i*50);
	})
})
```

This is a simple situation where you have created an atomic functionality that can be initiated by clicking a button in the UI. Clicking through each one of them manually if there are 100 of them on the screen is a pain. 

if you do `$(selector).click()` this will click all buttons simultaniously which can create a peak load on the server. The above code help helps you click all the buttons in the screen with a 50ms delay. 

Example usage
1. Create invoices from portal data in Mr Albert
![[CleanShot 2020-11-19 at 16.13.39.png]]

2. Run all checks in Mr Albert
![[CleanShot 2020-11-19 at 16.14.23.png]]