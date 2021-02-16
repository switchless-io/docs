# install NPM packages from local directory
--- 
- keywords: , [[npm]]
- author: #alex
--- 
```shell
npm install --save ../path/to/mymodule
```


```shell
npm install --save /Users/alex/ec2code/asyncauto/custom-importers
```

This copies the files to `node_modules`. So when you make changes, you will have to reinstall the package by uninstalling and then installing again. 


once installed, it will show up in 
```javascript
"mralbert_helper": "file:../mralbert_helper",
"custom-importers": "file:../custom-importers",
```

install from private git repo instead - [[Install private gitrepo as dependancy]]


ref: https://stackoverflow.com/a/38417065