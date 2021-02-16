# Iterating through an array like object

![[Pasted image 20201225142152.png]]

To iterate through each key here, use `for-of`


```
var p = {
    0: "value1",
    "b": "value2",
    key: "value3"
};

for (var key of Object.keys(p)) {
    console.log(key + " -> " + p[key])
}
```


More details here: https://stackoverflow.com/questions/684672/how-do-i-loop-through-or-enumerate-a-javascript-object