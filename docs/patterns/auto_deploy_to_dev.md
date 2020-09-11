# Auto deploy to Dev

It helps to keep deploying latest code to dev on a specific branch to dev server. It helps others test your code. 

Create folder - `.gitlab` and in that folder create file - `eb_config.yml` with the following content
```
global:
  application_name: MrAlbert app
  default_region: us-east-1
  profile: eb-cli
  sc: git
  workspace_type: Application
```

Create `.gitlab-ci.yml` and add the following instructions to it. 

```
image: asyncauto/nodejs_gitlab_ci:latest

stages:
  - testing_before_deploy
  - deploy
  - testing_after_deploy
deploy_to_dev:
  stage: deploy
  only:
    - develop
  environment:
    name: dev
  script:
   - mkdir ~/.aws/
   - touch ~/.aws/credentials
   - printf "[eb-cli]\naws_access_key_id = %s\naws_secret_access_key = %s\n" "$AWS_ACCESS_KEY_ID" "$AWS_SECRET_ACCESS_KEY" >> ~/.aws/credentials
   - touch ~/.aws/config
   - printf "[profile eb-cli]\nregion=us-east-1" >> ~/.aws/config
   - mkdir .elasticbeanstalk
   - mv .gitlab/eb_config.yml .elasticbeanstalk/config.yml
   - eb deploy mralbert-dev
```

Go to gitlab environment variables in your repo -> settings -> CI/CD -> variables and add these three variables 

```
AWS_ACCESS_KEY_ID
AWS_DEFAULT_REGION
AWS_SECRET_ACCESS_KEY
```
