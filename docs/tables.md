# Tables
Keywords:[[patterns]]

This document describes the most common table patterns that we use. 
This is over and on top of [formantic ui tables](https://fomantic-ui.com/collections/table.html)

### Non stackable 
By default semantic offers responsive tables. That however does not make much sense. Typically we want the table to look like a table on mobile as well. 

This one is non stackable but if the view port is small, then the right side of the table might not be visible
```
<table class="ui celled unstackable collapsing table">
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Site</th>
            <th>Device id</th>
        </tr>
    </thead>
    <tbody>
        <tr data-id=''>
            <td>name</td>
            <td>type</td>
            <td>site</td>
            <td>Device id</td>
        </tr>
    </tbody>
</table>
```

### Non stackable with horizonal scroll









