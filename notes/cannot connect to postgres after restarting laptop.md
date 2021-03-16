# Cannot connect to postgres after restarting laptop

This issue typically happens when the laptop shuts down unexpectedly. 

## Solution
```shell
postgres -D /usr/local/var/postgre

# kill the PID mentioned in the hint shown when you run the above
kill -9 PID 
```

Ref: 
https://stackoverflow.com/a/45352573