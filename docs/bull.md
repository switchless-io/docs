# Bull

## About
We use bull for queue up tasks. Two major reason why we use queues. 
1) something is expected to be heavy and we dont want to block the event loop
2) something is expected to fail and we want the option to retry it

Eg of case 1 is something that heavy process such running some shell scripts or running puppeteer etc. 

Eg of case 2 is a request to be made to a 3rd part that is expected to have a downtime or processing a webhook from a 3rd party system. 


## Setup
Use the [switchless cli](https://switchless.io/getting-started/) to setup bull. Our standard setup includes a UI for visualising the state of the queue. 


## Usage

### Sandboxed queue

> Sometimes jobs are more CPU intensive which will could lock the Node event loop for too long and Bull could decide the job has been stalled. To avoid this situation, it is possible to run the process functions in separate Node processes. In this case, the concurrency parameter will decide the maximum number of concurrent processes that are allowed to run.

> We call this kind of processes for “sandboxed” processes, and they also have the property that if the crash they will not affect any other process, and a new process will be spawned automatically to replace it.

ref: 

- [https://optimalbits.github.io/bull/#sandboxed-processors](https://optimalbits.github.io/bull/#sandboxed-processors)

#### When using sandboxed queue:
**1) Store all your processors in `/api/processors`**

here is an example of a processor that runs a shell script, picks up the data and creates a new queue item to process the data. 
```js
module.exports = function (job,callback) {
	var folder_name = __dirname;
	folder_name = folder_name.split('/api')[0];
	var options = job.data.options;
	var run_config = options.run_config;
	fs.writeFileSync(folder_name+"/automations/run_config.json", JSON.stringify(run_config,null,'\t'));
	fs.writeFileSync("./automations/data/gstr2a_"+run_config.client.gstin+".json", JSON.stringify([],null,'\t'));
	
	var q='node node_modules/.bin/codeceptjs run --steps -c '+folder_name+'/automations/codecept.conf.js -i '+folder_name+'/automations/new_get_gstr2a_details_auto.js'			
	shell.exec(q); 
	// read the file
	var filings = JSON.parse(fs.readFileSync(folder_name+'/automations/data/gstr2a_'+run_config.client.gstin+'.json'));
	if(filings.length==0)
		return callback(new Error('crawling failed - no data extracted'));
	// if file is empty the throw error
	var data={
		title:`Add portal data(${options.what}) to tracker - ${options.mode}`,
		options:{
			what:options.what, //'gstr3b',
			mode:options.mode, //'audit',
			gstin:options.gstin,
			run_config:run_config,
			filings:filings,
		},
	};
	promise = queue.add('add_portal_data_to_tracker',data);
	promise.then(function(result) {
		callback(null, filings);
	}, function(error) {
		callback(error);
	});

}
```

**2) Add process to `BullBootstrap.js`**

example: 
```js
queue.process('crawl_gstr3b',1,'/Users/alex/ec2code/asyncauto/mralbert/api/processors/crawlGSTR3B.js');
queue.process('crawl_gstr2a',1,'/Users/alex/ec2code/asyncauto/mralbert/api/processors/crawlGSTR2A.js');
```

**3) Update visual studio code's `launch.json` to be able to debug child process**
Add `autoAttachChildProcesses` to configurations.

```
{
    "type": "node",
    "request": "launch",
    "name": "local_test",
    "autoAttachChildProcesses": true, // add this 
    "program": "${workspaceFolder}/app.js",
    "outputCapture": "std",
    "env": {
        "REDIS_HOST":"localhost",
    }
},
```
VS code by default only setups debug for the main process. If you dont run this, the logic will not work when using the debug console on VS code. However if you run `npm start` via the terminal, it will work fine without making this change. Just that you will not be able to use the VS code debugger. 

## Ref: 
- [Bull official reference](https://github.com/OptimalBits/bull/blob/develop/REFERENCE.md)