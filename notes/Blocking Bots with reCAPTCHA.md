---
author: #anzal 
---
### Create an account
Create a developer's account and get the `site_key`
https://developers.google.com/

### Choosing a verification method
- reCaptcha v3 gives a score between 0 and 1
- reCaptcha v2 has Yes or No results for security check. There are two types
	- 'I'm not a robot'
	- invisible captcha 

Refer: https://developers.google.com/recaptcha/docs/versions

### Implement reCAPTCHA in front end
```
<form>
	<div class="g-recaptcha" data-sitekey="<%=sails.config.recaptcha.site_key%>"></div>


	<br>

	<input type="submit" value="Create Account" class='ui fluid circular button' style="margin-bottom: 0.7em;">


</form>
```

### Verify user's response from backend
https://developers.google.com/recaptcha/docs/verify

```
authenticateReCAPTCHA(req_body,callback){

var options = {

	method: "POST",

	url: `https://www.google.com/recaptcha/api/siteverify`,

	body:`secret=${sails.config.recaptcha.secret_key}&response=${req_body['g-recaptcha-response']}`,

	headers: { "Content-Type": "application/x-www-form-urlencoded" },



	};



	function cb(error, response, body) {

	if(response){

	callback(JSON.parse(body).success);

	}

	}



	request(options, cb);



},

```