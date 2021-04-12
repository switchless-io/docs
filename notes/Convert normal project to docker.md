---
author:#alex 
---

# Convert normal project to docker


## Create a dockerfile
File name - `Dockerfile`
File content: 
```
FROM node:12.16.3


# Create app directory
WORKDIR /usr/src/app

# Install app dependencies
COPY package.json .
# For npm@5 or later, copy package-lock.json as well
# COPY package.json package-lock.json .

RUN npm install

# Bundle app source
COPY . .

EXPOSE 1337

# CMD ["npm","run", "codeceptjs"]

CMD [ "npm", "start" ]
```

## Run docker build to create the image

```
 docker build -t cashflowy .
```

when you check for images with `docker images`, you should see your newly created image. 
![[CleanShot 2021-04-10 at 10.41.15.png]]

Expect the first build to take a long time. 

## create local config file for docker
`docker_local_env`

if you want to use resources from the host such as redis or postgres, instead of setting the host as `localhost`, set the host as `host.docker.internal`
eg:
```
DB_HOST=host.docker.internal
REDIS_HOST=host.docker.internal
```

Add `docker_local_env` to `.gitignore`

## Create a dockerignore file
file name - `.dockerignore`
content:
```
node_modules
npm-debug.log
```

## Grunt install issue
This was resolved when more packages was installed. Not sure how this happened. 

## 


