# Setup Web app

> this document is unfinished.

## About web app. 
This is most of the functionalities that we found useful in a customer facing web app. 

## Prerequisite

- install postgres - `brew install postgresql`
- install redis - `brew install redis`

## Create a new web app

**1) create a new sails project**
```shell
sails new switchless_project
cd switchless_project
```

**2) install switchless cli as a dev dependancy**
```shell
npm install --save-dev @switchless-io/cli@latest
```

**3) run switchless cli**
```shell
./node_modules/@switchless-io/cli/index.js
```
choose - initialise --> web-app

Switchless is a code generator. We are not installing packages here. We are overwriting parts of your sailsjs app - just as if you were customising your sailsjs app. 

**4) Create database**
```psql
sudo -u alex createdb mralbert_test -O rdsuser
```

**5) Lift the server**

Using VScode debugger, lift the server. A `launch.json` containing environment variables is added to your project. That contains basic environment variables needed to lift the server. 

Commit all these changes and get started with writing your business specific logic.
