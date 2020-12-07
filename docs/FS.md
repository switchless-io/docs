# FS
keyword : [[stack]], [[npm module]]

author: [[Alex]]

This is an npm module that we use working with file systems. 


## Get a working directory
```
var folder_name = __dirname;
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


## Read a file 
```
var crawl_data = fs.readFileSync(folder_name+'/automations/data/setup_gstin.json');
```


Related notes:
- [[How to use dirname]]