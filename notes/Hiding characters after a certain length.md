# Hiding characters after a certain length

---
- author: #anzal 
---


```javascript
text=text.replace(/(\w{3}).*/g, "$1"+(new Array(text.length -3 + 1).join( '*' )));

// this will convert 'Anzal' to 'Anz**'
```