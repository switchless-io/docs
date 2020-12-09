# How to change file upload size limit in Nginx
---
- Keywords:[[how to]][[nginx]]
- author: [[alex]]
---
- Nginx limits max file upload size to 1mb.  
- To increase that you need to set client_max_body_size param.  
- Example, for upload limit to be 10mb: client_max_body_size 10M;    
- In Beanstalk you can add this configuration via .ebextensions.  
 
 Steps:  

-  create a config file .ebextensions/upload_limit.config  
-  code to increase file limit  
```
files:  
  /etc/nginx/conf.d/upload.conf:
    mode: "000644"
    owner: root
    group: root
    content: |
      # config for file upload  
      client_max_body_size 10M;
```
-  commit the code.  
-  deploy  
