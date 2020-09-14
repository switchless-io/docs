# How to kill something running in a specific port?
**While starting the app, you might get an error similar to this:**  

`020-09-14T09:52:16.044Z - error:  -> Is something else already running on port 1337 ?
2020-09-14T09:52:16.044Z - error: 
2020-09-14T09:52:16.044Z - error:  -> Are you deploying on a platform that requires an explicit hostname, like OpenShift?
2020-09-14T09:52:16.045Z - error:     (Try setting the `explicitHost` config to the hostname where the server will be accessible.)
2020-09-14T09:52:16.045Z - error:     (e.g. `mydomain.com` or `183.24.244.42`)`

In this case kill the port from terminal and try again:

command to kill a port(1337 here) in mac is this:  
`sudo lsof -t -i tcp:1337 | xargs kill`  
  
For windows and linux machines, refer this thread: https://stackoverflow.com/questions/3855127/find-and-kill-process-locking-port-3000-on-mac


