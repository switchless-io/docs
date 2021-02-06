# Setup 2factor

- create an account. 
- Email contains instructions and API details. 

## Configure environment files
configure `development.js` and `production.js`
```javascript
two_factor:{
	api_key:process.env.TWO_FACTOR_API_KEY
},
```


## Create two factor service
```
var https = require('follow-redirects').https;
var fs = require('fs');





module.exports={
	generateOTP:function(phone,callback){
		var options = {
		  'method': 'GET',
		  'hostname': '2factor.in',
		  'path': `/API/V1/${sails.config.two_factor.api_key}/SMS/${phone}/AUTOGEN`,
		  'maxRedirects': 20
		};
		var req = https.request(options, function (res) {
			var chunks = [];

			res.on("data", function (chunk) {
			  chunks.push(chunk);
			});
			res.on("end", function (chunk) {
				var body = Buffer.concat(chunks);
				callback(null,body.toString());
			});

			res.on("error", function (error) {
				callback(error);
			});
		});

		req.end();
	},
	sendOTP:function(opts,callback){
		var options = {
		  'method': 'GET',
		  'hostname': '2factor.in',
		  'path': `/API/V1/${sails.config.two_factor.api_key}/SMS/${opts.phone}/${opts.otp}`,
		  'maxRedirects': 20
		};
		var req = https.request(options, function (res) {
			var chunks = [];

			res.on("data", function (chunk) {
			  chunks.push(chunk);
			});
			res.on("end", function (chunk) {
				var body = Buffer.concat(chunks);
				callback(null,body.toString());
			});

			res.on("error", function (error) {
				callback(error);
			});
		});

		req.end();
	},
	
	verifyOTP:function(opts,callback){
		var options = {
		  'method': 'GET',
		  'hostname': '2factor.in',
		  'path': `/API/V1/${sails.config.two_factor.api_key}/SMS/VERIFY/${opts.two_factor_session}/${opts.otp}`,
		  'maxRedirects': 20
		};
		var req = https.request(options, function (res) {
			var chunks = [];

			res.on("data", function (chunk) {
			  chunks.push(chunk);
			});
			res.on("end", function (chunk) {
				var body = Buffer.concat(chunks);
				callback(null,body.toString());
			});

			res.on("error", function (error) {
				callback(error);
			});
		});

		req.end();
	}
}
```