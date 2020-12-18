# Passing variables into a partial
---
- author: [[Alex]]

--- 

All variables referenced in partials can reference global variables. So most of the time as long as the variable is defined globally you dont need to explicitely send variables into a partial. But in case you are using the partial to render multiple versions of the data on the same page, this global variable scope strategy is not going to work. 

In such a case or as general good practice, send the variable into the partial scope. 
```
<%- include('partials/invoice', {i:invoice.transformed_import_data}); %>
```
