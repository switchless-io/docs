# Nginx

## Notes related to Nginx
- [[How to change file upload size limit in Nginx]]
- [[How to redirect a specific url to a page in different domain with nginx]]
- [[Run multiple apps locally with their own DNS map]]
- [[Set a password for an environment]]

## Common debug

### Check if Nginx config is error free

```
sudo nginx -t
```

When it has errors 
```
nginx: [emerg] unknown directive "server\_name" in /usr/local/etc/nginx/servers/my.config:3

nginx: configuration file /usr/local/etc/nginx/nginx.conf test failed
```

When it is all ok
```
nginx: the configuration file /usr/local/etc/nginx/nginx.conf syntax is ok
nginx: configuration file /usr/local/etc/nginx/nginx.conf test is successful
```

### brew service does start nginx properly
When you try to run nginx using brew it does not work
```shell
brew services start nginx
```
But when you try to start nginx using brew in sudo mode, it works

```shell
brew services start nginx
```

#### Solution
```shell
sudo chown -R alex /usr/local/var/log/nginx/
```