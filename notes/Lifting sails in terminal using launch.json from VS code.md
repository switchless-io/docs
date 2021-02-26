# Lifting sails in terminal using launch.json from VS code

sails is installed globally here - 
`/usr/local/lib/node\_modules`

Add this to the top of `/bin/sails.js`

```javascript
// ----- for using vs code config ---- 
var fs = require('fs');
var folder_name = process.cwd();
var launch_config = fs.readFileSync(folder_name+'/.vscode/launch.json').toString('utf8');
// console.log(typeof launch_config);
var Hjson = require('hjson');

var obj = Hjson.parse(launch_config);
// console.log();

var env ='local_test'; // use this configure which environment you want to use
// var env ='prod db';

var configuration;
obj.configurations.forEach(function(conf){
  if(conf.name==env)
    configuration=conf;
})

// console.log('\n\n\n-------configuration');
// console.log(configuration);
// console.log(obj);
// return;

Object.keys(configuration.env).forEach(function(key){
  process.env[key] = configuration.env[key];
})
// console.log(process.env);
// return;
// END ----- for using vs code config ---- 
```


You might have to correct 

https://stackoverflow.com/questions/5926672/where-does-npm-install-packages




