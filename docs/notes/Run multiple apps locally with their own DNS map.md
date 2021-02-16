# Run multiple apps locally with their own DNS map



## About
When you are working on multiple apps locally it can be a pain to remember the ports that they are running on. You can face this issue when you are running multiple sails servers or when you are running multiple mkdocs or eleventy server. 
![[CleanShot 2021-01-11 at 10.52.35.png]]


Both cashflowy and parsemonkey are running at the same time.

## Implementation details
```shell
#install nginx 
brew install nginx

#run nginx perpetually 
brew services start nginx

# configure nginx 
cd /usr/local/etc/nginx/
mkdir servers/
cd servers/

\# create your local traffic router via nginx 
vim my.config
```
  
```
\# add these lines to my.config 
server {
    listen 80;
    server_name parsemonkey.local;
    location / {
      proxy\_pass http://localhost:1000;
   }
  }

server {
    listen 80;
    server_name parsemonkey.local;
    location / {
      proxy\_pass http://localhost:1001;
   }
  }

server {
    listen 80;
    server_name mralbert.local;
    location / {
      proxy\_pass http://localhost:1001;
   }
  }
```
  
```
\# add the port env variable in launch.json 
"PORT": "1000" #parsemonkey
"PORT": "1001" #cashflowy
"PORT": "1002" #yoletters
"PORT": "1003" #mralbert
```
  
```
\# add DNS mapping for your macbook via vscode
code /etc/hosts

  

\# add these lines at the end of /etc/hosts file and save it

# Application DNS
127.0.0.1 parsemonkey.local
127.0.0.1 cashflowy.local
127.0.0.1 yoletters.local
127.0.0.1 mralbert.local
```
  

\# finally restart the nginx server
brew services restart nginx

**Want to add a new application to your DNS?**  
Just add each the additional configuration for nginx, launch.json, /etc/hosts.  Don't forgot to restart nginx. You are good to go.  
  
**\[Advance\]** **Run a https server locally**  
[https://blog.filippo.io/mkcert-valid-https-certificates-for-localhost/](https://blog.filippo.io/mkcert-valid-https-certificates-for-localhost/)