# Not able to connect to redis
#issue

## The issue looks something like this:
``` shell
debug: Warning: since `sails.config.session.cookie.secure` is not set to `true`, the session
debug: cookie will be sent over non-TLS connections (i.e. with insecure http:// requests).
debug: To enable secure cookies, set `sails.config.session.cookie.secure` to `true`.
debug: 
debug: If your app is behind a proxy or load balancer (e.g. on a PaaS like Heroku), you
debug: may also need to set `sails.config.http.trustProxy` to `true`.
debug: 
debug: For more help:
debug:  • https://sailsjs.com/config/session#?the-secure-flag
debug:  • https://sailsjs.com/config/session#?do-i-need-an-ssl-certificate
debug:  • https://sailsjs.com/config/sails-config-http#?properties
debug:  • https://sailsjs.com/support
debug: 
2021-01-05T04:35:29.017Z - error: A hook (`session`) failed to load!
2021-01-05T04:35:29.022Z - error: Failed to lift app: message=Took too long to connect to the specified Redis session server.
You can change the allowed connection time by setting the `timeout` input (currently 15000ms)., stack=Error: Took too long to connect to the specified Redis session server.
You can change the allowed connection time by setting the `timeout` input (currently 15000ms).
    at Timeout._onTimeout (/var/app/current/node_modules/machinepack-redis/machines/get-connection.js:166:66)
    at listOnTimeout (internal/timers.js:549:17)
    at processTimers (internal/timers.js:492:7), code=E_REDIS_CONNECTION_TIMED_OUT
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
WARNING: Something seems to be wrong with this function.
It is trying to signal that it has finished AGAIN, after
already resolving/rejecting once.
(silently ignoring this...)
 [?] For more help, visit https://sailsjs.com/support
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
```


## Resolution
Check the security group for redis. 
make sure port 6379 is accessible. 
![[Pasted image 20210105104612.png]]

ref: https://stackoverflow.com/questions/36169117/aws-elasticache-timeout-from-ec2

