# Mk Docs
---
- Keywords: #stack
- author: #alex
---
This is what we use to documenting things - both public documentation such as this and private documentations such in internal handbooks.

## Requirements of a documentation system 
- tooling should be familiar
- documentation should be done by the creator - in this case the developer
- tooling should be efficient for creator - ie should be developer friendly 
- A tooling that fits developers helps do multiple iterations of the same document. 

## What we tried before
We tried wordpress. The problem with wordpress is that, specifically for a developer, there is a lot of overhead. 
You will have to head over to a website, enter username password and then then write content. 
By the time you head over the browser, login, half of your enthusiasm for writing is gone. 
Also you are bothered by whether you should create a post or a page.

Lets look at the workflow in Mkdocs. 
You are writing code and you come across an interesting idea. You command tab to the right sublime window. Create a file and start writing. 
Once you are done, you can choose you organise it. you can choose to commit it if you like it. you can choose to let it be there for a while if you are not satisfied with it. 

The obvious disadvantage for a system like this is that it is only suited for developer writters. Its going to be super difficult for a non developer to contribute. 

## Our flavor of mkdocs 
[Swithless flavor of mkdocs](https://github.com/switchless-io/mkdocs)

## Getting started with Mkdocs

The generator for switchless is available in switchless-cli. Run the switchless cli to install mkdocs with our flavor.

**Pre-requesites:**
`sudo easy_install mkdocs` - installs mkdocs cli

### Setup documentation seperately 

```shell
# create a folder 
mkdir asyncauto_handbook

# setup up the folder. 
cd asyncauto_handbook

# Initialise git
git init

# Initialise npm and install switchless cli
npm init
npm install --save-dev @switchless-io/cli@latest

# Run the cli and install the latest theme of mkdocs 
./node_modules/@switchless-io/cli/index.js
# choose --> install --> mkdocs

# Lift the server
mkdocs serve

# create a remote repo and push data to repo
git commit -m "mkdocs setup"
git remote add origin https://github.com/your_name/your_repo.git
git push -u origin master
```

### Setup documentation in your existing node project

`./node_modules/@switchless-io/cli/index.js` 

choose `install`, choose `mkdocs` from the menu.

### Setup documentation in a new switchless app
If you are starting a new project, mkdocs in included in the `web-app` template.

`mkdocs serve` - you can view the static files that you are working on currently on your local browser. `localhost:8000`

## Hosting

### Public hosting using readthedocs
We generally prefer [readthedocs.org](https://readthedocs.org) for hosting public documentations. They have some additional features regarding versioning of documentations. 

**To deploy via readthedocs:**

- signup for an account on readthedocs
- point the cloudflare DNS to the newly created doc `Cname handbook.asyncauto.com --> cloudflare-to-cloudflare.readthedocs.io`
- connect your github repos to readthedocs
- click `import repository`

**Use the following settings**

- advanced settings
	- defaut version - latest
	- default branch - master
	- single version - tick this checkbox 
  - documentation type - mkdocs (default is sphinx, you need to change this)
- domains 
	- add your domain 
		- canonical - tick this checkbox
		- always use http - tick this checkbox 

#### Expected issues:

1. If you dont point the dns to `cloudflare-to-cloudflare.readthedocs.io` before setting up the project, you will experience some DNS propogation delays. 
2. Immediately after you setup your custom domain, you will get an ssl error. It takes a while for readthedocs to issue you an ssl certificate. Browser bar will show `Not Secure` for some time.


### Public hosting using s3
Use cloudflare and s3 to privately host your static files

Refer to this - [How to host a static website using AWS S3 and Cloudflare](https://miketabor.com/how-to-host-a-static-website-using-aws-s3-and-cloudflare/) to setup your static site. 

### Private hosting using aws s3

Perform the steps in the previous section
**Protection from cross domain access**
![s3 does not allow cross domain access](files/s3-does-not-allow-cross-domain-access.png)
Because of how s3 works, your bucket name should be the name of the domain where you host your static site. S3 will not allow any other domain to point to your s3 bucket. 

Add some content to the S3 bucket and you will be able to see the content on your new endpoint. 
2 more things to do:

1. Make it private - only someone from your team should be able to access it
2. Site should be updated when the repo is updated. 

#### Using Cloudflare access to restrict access to only your team
<div style="position: relative; padding-bottom: 56.25%; height: 0;"><iframe src="https://www.loom.com/embed/23c1eb1df7634e769217cc3c1ed4ff0d" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe></div>
Use cloudflare access to limit who can access your static site. Note cloudflare access is paid. If you dont want to pay for it, and if you want just basic access restriction, create a google group and set access policy to that group email address. Cloudflare will send an OTP to that email address. Anyone in the google group will be able to access your private docs. 

If you fancy paying for it, cloudflare access gives a lot more sophisticated access control.

#### CI/CD pipeline using Gitlab

**Configure your AWS credentails as environment variables**

Go to your repo on Gitlab. Go to `settings` --> `CI/CD` --> `Variables`
Add these variables: 

- AWS_ACCESS_KEY_ID
- AWS_DEFAULT_REGION
- AWS_SECRET_ACCESS_KEY

These environment are special for Gitlab. Gitlab automatically recognises them as AWS credentials and will automatically configure the runner with the AWS credentials. You dont have to manually apply these credentials in the runner. This will prevent your credentials from getting leaked into the logs. 

**Configure Gitlab config - .gitlab-ci.yml** 

Create a file called `.gitlab-ci.yml` in your repo and add the following content to it. 
```
image: ruby
deploy_to_s3:
 type: deploy
 image: ruby
 only: 
  - master
 script:
  - apt update
  - apt install -yq python3-pip nodejs git
  - pip3 install mkdocs>=1.1.2
  - mkdocs build --verbose
  - pip3 install awscli
  - echo "Pushing the static files"
  # - mkdir ~/.aws/
  # - touch ~/.aws/credentials
  # - printf "[eb-cli]\naws_access_key_id = %s\naws_secret_access_key = %s\n" "$AWS_ACCESS_KEY_ID" "$AWS_SECRET_KEY" >> ~/.aws/credentials
  - aws s3 sync public/ s3://agent-handbook.mralbert.in --exclude ".DS_Store/*" --cache-control "max-age=120000" --delete
```
Notice that 3 lines are commented out. Gitlab runnner automatically recognises that you are trying to work with AWS. Because of this you dont have to specify the AWS credentials in the runner script. Gitlab detects this based on the environment variables that you set via the UI.

## Usage 
- Write doc
- Organise it under folders etc
- Update the Navbar if required
- Commmit to repo

## Other notes related to Mkdocs
- [[Install plugins in Mkdocs]]
- [[Obsidian to Mkdocs conversion]]
- 

## Ref: 
- [https://www.mkdocs.org/user-guide/deploying-your-docs/](https://www.mkdocs.org/user-guide/deploying-your-docs/)