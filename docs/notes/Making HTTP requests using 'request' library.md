# Making HTTP requests using 'request' library
---
- Keywords:[[patterns]]
- author: #alex
---
Scenarios where we need to use request library:  
- We might need to make API calls from backend  
- We might need to submit forms from backend

Complete doc:https://www.npmjs.com/package/request

Code example:  
```
var request = require('request');
 

var user={
  name:'1test name',
  email:'1test_email@gmail2.com'
}

var options = {
  method: "POST",
  url: "https://us18.api.mailchimp.com/3.0/lists/1048219f9e/members",
  headers: {
    "authorization": "Basic <token here>",
    "cache-control": "no-cache",
    "postman-token": "8cd7409d-0bf7-2072-b7fe-7c6452d4fcdf"
  },
  body:"{\n\t\"email_address\":\""+user.email+"\",\n\t\"status\":\"subscribed\",\n\t\"merge_fields\":{\n\t\t\"FNAME\":\""+user.name+"\"}\n}"
};
 
function callback(error, response, body) {
  if(error){

    console.log(error);
  }
  if (!error && response.statusCode == 200) {
    var info = JSON.parse(body);
    console.log(info);

  }
}
 
request(options, callback);

```
