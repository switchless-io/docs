# Download file
---
- keywords: [[patterns]]
- author: #alex
--- 

## Install sails hook upload
`npm install sails-hook-uploads --save`


## Controller code
```
// something that generated the file
var time = new Date().getTime();
var out = XLSX.writeFile(wb, 'out_'+req.user.id+'_'+time+'.xls');


// the act of downloading the file. 
res.attachment('invoice.xls');
var downloading = await sails.startDownload('out_'+req.user.id+'_'+time+'.xls');
downloading.pipe(res);
```

Timestamp is added to the filename so as to avoid race conditions between 2 requests trying to download a file simultaniously. Timestamps are likely to be more unique. Avoid race conditions further by appending user id to the file name as well. 

## In production.js, explicitly set the adapter
You will need to specify which adapter to use explicity in `production.js`. Else it will error out when lifting the server in production mode. 
```
uploads:{
	adapter:require('skipper-disk'),
}
```

If you are uploading files to S3, then you will need to use `skipper-s3` instead. Ref to [[Upload a file]]. 

## ref: 
- https://sailsjs.com/documentation/reference/response-res/res-attachment
- https://github.com/sailshq/skipper#use-cases
- 
