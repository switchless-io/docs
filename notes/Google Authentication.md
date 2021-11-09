# Objective
Enable Google log in

# Implementation
1. Create a google cloud project
	1. Create credentials with right redirect URLs and origins![[Pasted image 20211109163623.png]]
	2. Set up 'Oauth Consent Screen' settings![[Pasted image 20211109163100.png]]
	3. Make sure that the scope contains email and profile![[Pasted image 20211109163225.png]]
2. Set up the app routes
	1. 'GET /auth/google/callback': 'AuthController.gloginCallback' 
	2. 'GET /auth/google': 'AuthController.glogin',
	3. 'POST /auth/google': 'AuthController.glogin',

3. Set up the controller actions:

```glogin: function (req, res) {

if (req.user)

return res.redirect('/');

	passport.authenticate('google', { scope: ['email', 'profile'] })(req, res);

},

gloginCallback:function(req,res){

	passport.authenticate('google', {failureRedirect: '/login',successRedirect:'/' })(req,res)

},
```
4. Set up PassportService.js

install `passport-google-oauth20`

```const GoogleStrategy = require('passport-google-oauth20').Strategy;
  
  

function extractProfile(profile) {

	let imageUrl = '';

	if (profile.photos && profile.photos.length) {

	imageUrl = profile.photos[0].value;

	}

	return {

	id: profile.id,

	displayName: profile.displayName,

	email: profile._json.email,

	image: imageUrl,

	};

}

passport.use(new GoogleStrategy({

	clientID: '584359031459-ev6395v28rja7rg9s501jmi9ln70c1o9.apps.googleusercontent.com',

	clientSecret: 'AZiTgLo6qpU1D8sr8C132BBK',

	callbackURL: `${sails.config.app_url}/auth/google/callback`,

	accessType: 'offline',

	userProfileURL: 'https://www.googleapis.com/oauth2/v3/userinfo',

	},function(token, tokenSecret, profile, callback) {

	var u=extractProfile(profile)

	User.findOrCreate({ email: u.email.toLowerCase() },{

		name:u.displayName,

		email:u.email,

	}).exec(function (err, user) {

		if (err) { return callback(err); }

		if (!user) {

			return callback(null, false, { message: 'Incorrect email.' });

		}



		var returnUser = {

			email: user.email,

			createdAt: user.createdAt,

			id: user.id

			};

			return callback(null, returnUser, {

			message: 'Logged In Successfully'

		});


	});

}));


```