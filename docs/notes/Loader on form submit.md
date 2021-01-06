# loader on form submit
--- 
- keywords: [[form]], #pattern
- author: #alex
--- 
```
$('.ui.form').form({
	fields:{
		name:'empty',
		username:'empty',
	},	
	onSuccess:function(e,fields){
		$(this).addClass('loading');
	},
});

```


![[Pasted image 20201201125209.png]]