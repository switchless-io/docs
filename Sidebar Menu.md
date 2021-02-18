# Sidebar Menu

---
- author: #anzal  
---

## Appearance
**Closed**
![[Pasted image 20210216153637.png]]

**Open**
![[Pasted image 20210216153654.png]]

## Implementation
In the layout, enclose the page
```html
<body\> 
	<div class\="ui sidebar inverted vertical menu"\> 
		<a class\="item"\> 1 </a\> 
		<a class\="item"\> 2 </a\> 
		<a class\="item"\> 3 </a\> 
	</div\> 
	<div class\="pusher"\> <!-- Site content !--> </div\> 
</body\>


```


in javascript, trigger this code on a button press:
```javascript
$('.ui.sidebar') .sidebar('toggle') ;
```

