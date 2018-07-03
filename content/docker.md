---
title: Docker
image: /images/docker.png  
featured: true
author: carlos
date: Tue Jul 03 2018 10:11:45 GMT+0100 (IST)
tags:
  - programming  
  - docker  
  - containers
---

# Docker

`docker history <image_name>` will show the commands that make up the docker image and the size of each. Its good for knowing what to try and work on to shrink the size  
`docker inspect <image_name>`   
`docker top <container>` will show processes running in container
Host root =/= Conatiner root  
Remap UIDS in docker with --userus-remap



### Best Practices
 
 * Use official images  
 * keep image small  
 * Be specific. Dont use `:latest` as this can update automatically, or be old.  
 * UID and GID passed to container must already exist in container. 
 * you can run the `chown` command when running the `copy` to cut down on the size of the image
 * `-e` pass in environment variables of `docker container run`  
 * `docker history <image_name>` will show the commands that make up the docker image and the size of each. Its good for knowing what to try and work on to shrink the size  
 * `docker inspect <image_name>`  
 * `docker top <container>` will show processes running in container  
 * `docker stats <container>`  
 * `docker port <container>` 
 * `docker network ls / inspect / create --driver / connect / diconnect`  
 * can choose which network to attach to when starting a container. 
 * `docker network`:  
   * naming is crucial
   * docker defaults the hostname to the containers name but you can also set aliases.  
   * If you set up a new network on docker the names of the containers are visible to other containers on the network

