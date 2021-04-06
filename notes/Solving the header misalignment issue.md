---
author: #anzal 
---

# Solving the header misalignment issue

Data-tables have a misalignment problem with large tables:

![[Pasted image 20210406215126.png]]

we need it to appear like this:
![[Pasted image 20210406215151.png]]



## Solution:

Initialize tables in this manner:
```javascript

$(document).ready(function(){

	var table=$('#table_id').DataTable({

	})

	table.draw();

})
```

