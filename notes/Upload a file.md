# Upload a file
---
- author: #anzal
--- 


## Front end
form should be enctype - multipart/form-data
```html
<form class="ui form" method="POST" enctype="multipart/form-data">
```

input field format:
```html
<input type="file" name="file_pan_card" >
```
![[Pasted image 20201216094941.png]]
## Dependency
1. skipper-s3 library
```console
npm install skipper-s3
```

2. s3 files bucket 
	- create a bucket in AWS>s3![[Pasted image 20201216103624.png]]
	- it's okay if the sub folders doesn't exist, it'll be created during file creation

## Backend
```javascript
uploadPANOriginalFileToS3:  function(cb){

		req.file('file_pan_card').upload({
			// ...any other options here...
			adapter: require('skipper-s3'),
			key: process.env.AWS_ACCESS_KEY,
			secret: process.env.AWS_ACCESS_SECRET,
			bucket: process.env.S3_FILES_BUCKET+'/pan_cards',
			region: 'us-east-1',
		},function (err, uploadedFiles) {

			if(err)
				cb(null)

			// If no files were uploaded, respond with an error.
			if (uploadedFiles.length === 0){
				console.log('No file was uploaded');
			}

			console.log('uploaded file:');
			cb(null, uploadedFiles)
		});
},

```

save the returned file path somewhere
```javascript
if(results.uploadPANOriginalFileToS3
&&results.uploadPANOriginalFileToS3.length>=1){
	va.details.docs.pan_card=`pan_cards/${results.uploadPANOriginalFileToS3[0].fd}`
}

```


## Retrieving the file
**Front-end:**
```html
<a href="/documents/<%=_.get(user,'details.docs.pan_card')%>">Link to File</a>
```

**Back-end:**
Routes.js
```javascript
'GET  /documents/:folder_name/:document_id': {
	  action: 'findOneDocument',
	  controller: 'DocumentController',
	  skipAssets: false
}
```

DocumentController.js
```javascript

const AWS = require('aws-sdk');
module.exports = {
    findOneDocument: function (req,res) {

        if (!req.params.document_id) return res.status(400).json({
            message: 'Invalid params, s3_id is mandatory',
            status: 'failure'
        });

        
		var s3_name = req.params.folder_name+'/'+req.params.document_id;



		AwsService.get_object(s3_name, function (err, data) {
			if (err) return res.send(err);
			res.set("Content-Length", data.ContentLength).set("Content-Type", data.ContentType);
			return res.send(data.Body);
		});
    
    },

};

```



