# loader on form submit
--- 
- keywords: [[form]], [[ui pattern]]
- author: [[Alex]]
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