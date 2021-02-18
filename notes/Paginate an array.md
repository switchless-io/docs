# Pagination with array
---
- author: #anzal
- tags: 
---


```javascript
function paginate(array, page_size, page_number) {
  // human-readable page numbers usually start with 1, so we reduce 1 in the first argument
  return array.slice((page_number - 1) * page_size, page_number * page_size);
}

//call the paginate function to get items of a page
console.log(paginate([1, 2, 3, 4, 5, 6], 2, 2));
```