# ajv
keywords: [[stack]], [[npm module]], [[JSON schema validation]]

author: [[Alex]]

```javascript
var Ajv = require('ajv'); 
var ajv = new Ajv({ allErrors: true }); // options can be passed, e.g. {allErrors: true}
var test = ajv.compile(schema);
if(!test(filings)){ // if the schema validation does not pass
	var time = new Date().getTime();

	throw new Error('schema validation failed. data - '+process.env.SERVER_HOST+'/output/job_'+job.id+'_data_'+time+'.json - '+ 'Issue -' + test.errors[0].keyword +': '+test.errors[0].dataPath+' '+test.errors[0].message+ ' - '+JSON.stringify(test.errors));
}
```
