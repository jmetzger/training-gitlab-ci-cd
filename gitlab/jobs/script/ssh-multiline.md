# SSH connection to server executing commands (Including multiline) 

## create good.sh in root-folder of repo (git) 

```
#!/bin/bash

echo "good things start now"
ls -la
date

```

## Create gitlab-ci.yml 

```
workflow:
  rules:
    - if: '$CI_PIPELINE_SOURCE == "web"'

default:
  image: maven:latest

stages:          # List of stages for jobs, and their order of execution
  - deploy 
  
deploy-job:
  
   stage: deploy   
   image: ubuntu 

   variables:
     # GIT_STRATEGY: none
    CMD: |
      echo hello-you; 
      ls -la;

   before_script:
    - apt -y update
    - apt install -y openssh-client
    - eval $(ssh-agent -s)
    - echo "$TOMCAT_SERVER_SSH_KEY" | tr -d '\r' | ssh-add -
    - ls -la
    - mkdir -p ~/.ssh
    - chmod 700 ~/.ssh
    - ssh-keyscan $TOMCAT_SERVER_IP >> ~/.ssh/known_hosts
    - chmod 644 ~/.ssh/known_hosts
    - echo $TOMCAT_SERVER_SSH_KEY

   script:
    #- chmod 600 id_rsa
    #- scp -i id_rsa -o StrictHostKeyChecking=no target/*.war root@$TOMCAT_SERVER_IP:$TOMCAT_SERVER_WEBDIR 
     # - scp -o StrictHostKeyChecking=no target/*.war root@$TOMCAT_SERVER_IP:$TOMCAT_SERVER_WEBDIR
     # - cd $TOMCAT_SERVER_WEBDIR
     # - ls -la
     - echo 'V1 - commands in line'
     - ssh root@$TOMCAT_SERVER_IP -C "ls -la; cd /var/lib/tomcat9/webapps; ls -la;"
     - echo 'V2 - content of Variable $CMD'
     - ssh root@$TOMCAT_SERVER_IP -C $CMD
     - echo 'V3 - script locally - executed remotely'
     - ssh root@$TOMCAT_SERVER_IP < good.sh
     - echo 'V4 - script in heredoc'
     - |
      ssh root@$TOMCAT_SERVER_IP bash -s << HEREDOC
        echo "hello V4"
        ls -la
      HEREDOC

```
