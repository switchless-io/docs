# Bearer Auth
---
- keywords: #pattern
- author: #alex
---
We use this for user based access to backend apis. This auth can be applied to both blueprint APIs and well as custom APIs. 

The bearer token that we use is in fact a JWT token. The following are the features supposed by Bearer JWT Auth: 

- Aiblity to verify tokens with secret using JWT
- Abilty to create user specific tokens that only has access to resources that the user can access. 
- Ability to invalidate past tokens

## Setup 
**1) Install these packages:**
```js
passport-http-bearer
sails-hook-organics

```

2) Add this controller to Auth controller
```js
appLogin:function(req,res){
    if(!req.body.email)
        return res.badRequest('you need to specify email');
    if(!req.body.password)
        return res.badRequest('you need to specify password');
    User.findOne({ email: req.body.email }, function (err, user) {
        if (err) 
            throw err;
        if (!user)
            return res.status(401).json({ message: 'Incorrect email.' });

        bcrypt.compare(req.body.password, user.password, function (err, result) {
            if (!result)
                return res.status(401).json({message: 'Invalid Password'});
            var uuid = sails.helpers.strings.uuid();
            var token = jwt.sign({ id: user.id, uuid: uuid }, sails.config.api_jwt_secret);
            var details = user.details;
            if(!details.api)
                details.api={};
            if(!details.api.valid_uuids)
                details.api.valid_uuids=[];
            details.api.valid_uuids.push(uuid);
            User.updateOne({id:user.id},{details:details}).exec(function(err,result){
                res.send({token:token});
            })
        });
    });
},
```

3) Add this to `PassportService.js`

```
var BearerStrategy = require('passport-http-bearer').Strategy;
const jwt = require('jsonwebtoken'); 


/**
 * api token strategy.
 */
passport.use(new BearerStrategy(
    function (api_token, done) {
        jwt.verify(api_token, sails.config.api_jwt_secret, function (err, jwt_decode_payload) {
            if (err) return done(err);
            
            User.findOne(jwt_decode_payload.id).exec(function (err, user) {
                if (err) return done(err);

                if (!user) return done('user not found');

                //check for the uuid of the token with database
                var valid_uuids=_.get(user,'details.api.valid_uuids',[]);
                if (!valid_uuids.includes(jwt_decode_payload.uuid))
                    return done('your token is not part of acceptable tokens associated with this user.');

                // set the scope for the policy to indentify a blueprint request.
                return done(null, user, { scope: 'blueprint' });
            })
        })
    }
));
```

4) Modify `http.js`

```js
// modify http.order to the following
order: [
    'cookieParser',
    'session',
    'passportInit',     
    'passportSession',
    'authenticateBearer', // this is newly added
    'bodyParser',
    'myRequestLogger',
    'handleBodyParserError',
    'compress',
    'methodOverride',
    'poweredBy',
    'router',
    'www',
    'favicon',
    '404',
    '500'
],

// add this to http.middlewear
authenticateBearer: function (req, res, next) {
    // authenticate apis with bearer token

    if(req.headers.authorization && req.headers.authorization.startsWith('Bearer'))
        require('passport').authenticate('bearer', { session: false })(req, res, function(err){
            if(err){
                // console.log('Error while authenticating using Bearer token');
                // console.log(err);
                var myRequestLogger =require('@switchless-io/util').middleware.requestLogger;
                myRequestLogger(req,res,function(some_err){ // this will log the item to logger
                    return res.status(401).send(err);
                })
            }else{
                next();
            }
        });
    else
        next()
},

```

5) create a new policy - `isAuthenticatedViaAPI`
```js
module.exports = function(req, res, next) {
   if (req.isAuthenticated()) {
        return next();
    }
    else{
        return res.status(401).send('Use JWT Bearer token to authneticated yourself');
    }
};
```
This will check if the user is authenticated and send an appropriate error. 

6) Create a new policy - `canAccessThisOrgViaAPI`
```js
var async= require('async');
module.exports = function (req, res, next) {
    console.log(req.params);
    
     if (_.includes(sails.config.admins, req.user.email)) 
         return next();
    async.auto({
        // get all orgs that the user is part of
        getAllAccess:function(callback){
            Access.find({user:req.user.id}).exec(callback);
        }
    },function(err,results){
        var orgs=_.map(results.getAllAccess,'org');
        req.query.org=orgs;
        next(err);
    })
        
};
```
This policy is what you can modify to restrict access to resources based on user previlages. In this policy, if the user is an admin, then she will have access to all devices. Any other user will have only access to devices in the same org. This is done by setting req.query.org to orgs that the user is part of. 

7) Modify `policies.js`

```js
    APIController:{
        '*':['isAuthenticatedViaAPI','canAccessThisOrgViaAPI'],
    },
    UserController:{
        '*':['isAuthenticatedViaAPI','canAccessThisOrgViaAPI'],
    },
    OrgController:{
        '*':['isAuthenticatedViaAPI','canAccessThisOrgViaAPI'],
    },
    DeviceController:{
        '*':['isAuthenticatedViaAPI','canAccessThisOrgViaAPI'],
    },
    SiteController:{
        '*':['isAuthenticatedViaAPI','canAccessThisOrgViaAPI'],
    },
    MetricController:{
        '*':['isAuthenticatedViaAPI','canAccessThisOrgViaAPI'],
    },
    DispenseController:{
        '*':['isAuthenticatedViaAPI','canAccessThisOrgViaAPI'],
    },
```
Apply all these 2 policies to Controllers that matter to you. 

8) Add this to `routes.js`
```
'POST /app_login': 'AuthController.appLogin',
```

9) Modify your environment variables - `development.js` & `production.js`


## Usage

Make a `POST` request to `/api_login` to get the Bearer token. 

Include the Bearer token in the authorisation header. 
```
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6NCwidXVpZCI6ImMwNGM1YmZmLWFhNGYtNGU2OC1iNjk1LWI1ZWZmZmVlNjNjZCIsImlhdCI6MTU5NjU0NDIyOH0.Y42sktgmJ8PqTxx1KhlStXWU-orzy7Ia0ZQXiZt6aV0
```
