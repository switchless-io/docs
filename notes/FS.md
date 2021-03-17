# FS
---
- keyword : #stack
- author: #alex
---
This is an npm module that we use working with file systems. 

## Get a working directory
```
var folder_name = __dirname;
```

## Get process directory
```
var appPath = process.cwd();
```


## Check if a folder exists

```
var dir = folder_name+"/automations/data";
if (!fs.existsSync(dir)){
	fs.mkdirSync(dir);
}
```

## Write a file
```
fs.writeFileSync(folder_name+"/automations/data/error.txt", '');
```

### Append to a file 
```
fs.appendFileSync('message.txt', 'data to append');
```

## Read a file 
```
var crawl_data = fs.readFileSync(folder_name+'/automations/data/setup_gstin.json');
```


### Read file line by line
```
const fs = require('fs');
const readline = require('readline');
var folder_name = __dirname;

const fileStream = fs.createReadStream(folder_name + "/filings.txt");
const rl = readline.createInterface({
	input: fileStream,
	crlfDelay: Infinity
});
await async.eachLimit(rl,3,async function(line){
	console.log(line);
})
```

## Get list of files in a directory
```
var files = fs.readdirSync(directoryPath);
```

## Get file size
```
var stats = fs.statSync("myfile.txt")
var fileSizeInBytes = stats.size;
```

## Related notes:
- [[How to use dirname]]