# Disabling sort on certain columns
---
- author: #anzal 
---
## Appearance
see that last 3 columns don't have sort option
![[Pasted image 20210219131341.png]]

## Implementation
Add this script to disable sort in columns with class 'nosort'

```javascript
var table = $('#example').DataTable({
   'aoColumnDefs': [{
        'bSortable': false,
        'aTargets': ['nosort']
    }]
});
```


Add the class to the column in header

```html
<table>
    <thead>
        <tr>
            <th>Foo</th>
            <th>Bar</th>
            <th class="nosort">Baz</th>
        </tr>
    </thead>
    <tbody>...</tbody>
</table>
```
