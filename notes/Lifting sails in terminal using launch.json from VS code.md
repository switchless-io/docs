# Lifting sails in terminal using launch.json from VS code

sails is installed globally here - 
`/usr/local/lib/node\_modules`

Add this to the top of `/bin/sails.js`

```javascript
// ----- for using vs code config ---- 
var fs = require('fs');
var folder_name = process.cwd();
var launch_config = fs.readFileSync(folder_name+'/.vscode/launch.json').toString('utf8');
console.log(typeof launch_config);
var Hjson = require('hjson');

var obj = Hjson.parse(launch_config);
// console.log();
Object.keys(obj.configurations[1].env).forEach(function(key){
  process.env[key] = obj.configurations[1].env[key];
})
console.log(process.env);
// return;
// END ----- for using vs code config ---- 
```


You might have to correct 

https://stackoverflow.com/questions/5926672/where-does-npm-install-packages




