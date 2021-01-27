# Elastic search 


- Setup elastic search
	- t3


## Logging setup 

[[Setup Elasticsearch]]
[[Setup kibana]]
- kinesis role needs to be added to all access. - https://docs.aws.amazon.com/elasticsearch-service/latest/developerguide/fgac.html#fgac-mapping
[[Setup kinesis]]



1) Install switchless-cli in your sails project
```shell
npm install --save-dev @switchless-io/cli@latest
```

2) Update sails-helper to the latest version
```shell
npm install @switchless-io/util@latest --save
```

3) Go to the root directory of your sails project and run
```shell
./node_modules/@switchless-io/cli/index.js
```
4) Choose install-> logging 
![[Pasted image 20210127174335.png]]

7) Attach ==AmazonKinesisFirehoseFullAccess== policy to the ==aws-elasticbeanstalk-ec2-role== role


Ref: 

[Setup server logging](file:///Users/alex/Library/Mobile%20Documents/com~apple~CloudDocs/Basecamp-export-Async%20Auto-11-%202-2020/async-auto-hq-11695312/docs-and-files/setup-server-logging-2382992784.html)



Debug:

- use the test to see if you are able to send data to Elastic search. 
	- Amazon Elasticsearch Service Logs