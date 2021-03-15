# measure execution time with process.hrtime()

```
var hrstart = process.hrtime();

// piece of code to measure time goes here. 

var hrend = process.hrtime(hrstart);
console.info(`time taken - ${(hrend[0]*1000+hrend[1] / 1000000).toFixed(2)}ms` )
```

This can be used in asynchronous operations as well. 