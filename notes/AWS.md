# AWS
author: #alex 

aka amazon web services


## setup 
- [[setup a single instance]]
- [[AWS amzon linux 2 migration]]
- [[Refresh AWS Access Keys]]
- [[How to create AWS access keys]]
- [[Initialize EB CLI]]
- [[Set up ElasticBeanstalk Locally]]


## Issues
- [[Not able to connect to Redis]]
- [[Not able to connect to Postgres]]


## Cost Management
- [[]]

## config for Elastic search 
```javascript
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": [
          "arn:aws:iam::411068173358:user/programatic_access",
          "arn:aws:iam::411068173358:user/pa_mralbert",
          "arn:aws:sts::411068173358:assumed-role/Cognito_cashflowyInternalsoftwareAuth_Role/CognitoIdentityCredentials"
        ]
      },
      "Action": "*",
      "Resource": "arn:aws:es:us-east-1:411068173358:domain/asyncauto-prod/*"
    }
  ]
}
```