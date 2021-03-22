---
author:#alex
---

# Basic docker cheatsheet
keyword: [[docker]], [[cheatsheet]]

## Note: 

## Flags: 
 - d - run the container in detached mode (in the background)
 - p - 2000:80 map port 2000 on local machine to port 80 of the container


```
docker run -d -p 80:80 docker/getting-started
```

name the container while running it
```
docker run -d -p 2000:80 --name testname docker/getting-started
```

docker build
```
 docker build -t crawler .
```
docker build options
- t - for tagging in this format `name:tag`
- f or --file - this is where the 

to see a list of images 
```
docker images
```

To see all processes running 
```
docker ps
docker ps -a
```

to enter docker file system
```
docker exec -t -i elegant_poitras /bin/bash
```

![[Pasted image 16.png]]

`docker start <container name>`
`docker stop <container name>`
`docker rm <container name>`

Images and container names
![[CleanShot 2020-08-08 at 16.51.31.png]]


`docker logs <conatiner name>`
`docker logs -f <conatiner name>`


docker push image name
docker tag local stuff with global stuff 

`docker pull <image name>`

`docker-compose up -d` - looks for `docker-compose.yml` . In the YML you will specify what you would have written in docker run params.  


remove all docker images
`docker rmi $(docker images -a -q)`


Pushing things to docker hub
```
docker tag alex-custom:tagname alexjv89/test:tagname
docker push alexjv89/test:tagname


docker tag alex-custom alexjv89/test
docker push alexjv89/test:latest
```



Now add a new file called .dockerignore to your project’s root directory. The .dockerignore specifies which files and folders to ignore in the COPY step. In the .dockerignore, add the 2 lines below to ignore node modules and the npm debug log.

```
node_modules
npm-debug.log
```

Basic walkthough on how to deploy a docker container to docker - https://medium.com/@sommershurbaji/deploying-a-docker-container-to-aws-with-elastic-beanstalk-28adfd6e7e95

Enter cli of the docker container 
`docker exec -it quizzical_yalow /bin/sh`

Connect from container to a service on the host
https://docs.docker.com/docker-for-mac/networking/#use-cases-and-workarounds

passing env from host to container 
https://vsupalov.com/docker-environment-variables-from-host/#:~:text=You%20can%20pass%20the%20values,e%20var_name%20(...)

## Running mr Albert crawler

```
docker build -t crawler .
```
      
```
docker run --env-file=docker_local_env crawler
```

```
docker run -d -p 1337:1337 --env-file=docker\_local\_env crawler
```