---
title: Mastering Docker
image: /images/docker.png  
imageMeta:
  attribution:
  attributionLink:
featured: true
author: carlos
date: Tue Sep 11 2018 13:05:06 GMT+0100 (IST)
tags:
  - programming  
  - docker  
  - containers
---

## Mastering Docker  

Notes taken from Mastering Docker second edition by Russ McKendrick & Scott Gallagher  

##### ADD
`ADD` automatically uploads uncompresses, and puts the resulting folders and files at the path we tell it to.   
The `ADD` command can also be used to add content from remote sources.  
Archive files from a remote source are treated as files and are not uncompressed, so you will have to take this into account when using them.  
    
---  

 * Use `.dockerignore` to keep things out of Dockers build context. It will reduce the image size.  
 * Keep image as small as possible. Only install what is necessary.  
 * Execute only one application process per container.  

##### BUILD  

 * `-t` : tag/name image  
 * You can build your own image from scratch using the `FROM scratch` command  


##### Environmental Variables
To use environmental variables in your Dockerfile use the `ENV` instruction.    
`ENV <key> <value>` or `ENV <key>=<variable>`  
Using the second version of the above means you can set multiple variables on one line.  
`ENV username=admin database=db1 tableprefix=pr2_`  
