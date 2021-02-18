# Pick n elements from an array randomly

---
- author: #anzal
- tags: 
---


Say, for example, you have a large question bank and you want to select 10 questions out of them randomly. Here's how to do it:


```javascript
// Shuffle array
const shuffled = array.sort(() => 0.5 - Math.random());

// Get sub-array of first n elements after shuffled
let selected = shuffled.slice(0, n);
```