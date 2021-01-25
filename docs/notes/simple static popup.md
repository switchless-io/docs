# Simple static popup
---
- author: #alex 
---

Simply add `data-content="Add users to your feed"` to the element that you want to have popup.

```html
<div class="ui icon button" data-content="Add users to your feed">
  <i class="add icon"></i>
</div>
```

```javascript
$('.item .content .header').popup();
```

