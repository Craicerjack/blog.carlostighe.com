---
title: Bashrc
image: /images/ubuntu.png  
imageMeta:
  attribution:
  attributionLink:
featured: true
author: carlos
date: Mon Oct 22 2018 16:13:26 GMT+0100 (IST)
tags:
  - programming
  - terminal
---

# My Profile. 

Working away on my laptop and I just had the thought that I need to track my `.bashrc` or `.bash_profile` again. I have so many shortcuts in there that Im so used to that switching machines without them would be hella hassle so ....  

alias's:  
```  
alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF'
alias lash='ls -lash'  
alias grep="grep --color=auto"
alias rm="rm -i"
alias pyser="python -m SimpleHTTPServer"
alias phpser="php -S localhost:5000"
alias cds="cd sites/"
alias runserver="python manage.py runserver -dr"  

# reload shell
alias reload="source ~/.bashrc"  

# virtualenv shorts
alias w="workon "
alias de="deactivate && cd"
alias server="mysql.server start"
```

##### GIT commands
Add git branch to prompt:  
```
parse_git_branch() {

    git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'

}
export PS1="\[$txtcyn\]\u: \[$txtwht\]\w \[$txtgrn\]\$(parse_git_branch) $ \[\e[0m\]"  
```  

git alias commands:  
```  
# git commands
alias gs="git status"
alias ga="git add"
alias gc="git commit -m "
alias gch="git checkout"
alias gb="git branch"
alias pull="git pull origin"
alias push="git push origin"
alias rmdel="git ls-files --deleted -z | xargs -0 git rm"   
```  


#### Docker commands  
```  
dockbuild() {
    echo "building: $1";
    docker build -t registry/$1 .
    echo "Pushing: $1";
    docker push registry/$1
}
dockb() {
    echo "building: $1";
    docker build -t registry/$1 .;
}
dockp() {
    echo "Pushing: $1";
    docker push registry/$1;
}
dockstop() {
    echo "stopping: $1";
    docker stop "$1";
    echo "removing: $1";
    docker rm "$1";
}

alias dockremove="~/dockrm.sh"  
```  


