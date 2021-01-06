# How to redirect a specific url to a page in different domain with nginx
---
- Keywords: #pattern ,
- Author: #anzal
---

Edit the file .ebextensions/nginx_for_prod.config:

**Add a location handling config entry:**
set the proxy_pass to the url of the domain
```javascript
location /deals {
	proxy_pass https://wishup-holiday-season-deals.mailchimpsites.com/;
}

```

**Note:**
- if the url ends with /
it goes the the specified url

```
proxy_pass https://wishup-holiday-season-deals.mailchimpsites.com/;

```
this goes to https://wishup-holiday-season-deals.mailchimpsites.com/

- if the url doesn't end with /
it goes to the url+path 
```
proxy_pass https://wishup-holiday-season-deals.mailchimpsites.com;

```
this goes to https://wishup-holiday-season-deals.mailchimpsites.com/deals



**Example file content:**
```
files:
  /etc/nginx/conf.d/proxy_prod.conf:
    mode: "000644"
    owner: root
    group: root
    content: |
      # config for file upload
      client_max_body_size 20M;
      server {
        listen 8080;
        listen [::]:8080;
        server_name www.wishup.co;
        location /deals {
                proxy_pass https://wishup-holiday-season-deals.mailchimpsites.com/;
        }
        location / {
                proxy_pass  http://nodejs;
                proxy_set_header   Connection "";
                proxy_http_version 1.1;
                proxy_set_header        Host            $host;
                proxy_set_header        X-Real-IP       $remote_addr;
                proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;
        }
      }

```