# SSH connection to server executing commands (Including multiline) 

## Preparation on Server 

### Step 1: Create public/private key 

```
# on destinationn server
ssh-keygen
cd .ssh
ls -la
```

### Step 2: Add id_rsa.pub /Public key to authorized_keys 

```
cat id_rsa.pub >> authorized_keys
```

### Step 3: Add id_rsa (private key) to GITLAB ci/cd -> Settings -> CI/CD as new Variable 
```
cat id_rsa
# copy content and add as content to new variable SERVER_SSH_KEY
# DO not set variable as protected 
```

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

stages:          # List of stages for jobs, and their order of execution
  - deploy 
  
deploy-job:
  
   stage: deploy   
   image: ubuntu 

   variables:
    CMD: |
      echo hello-you; 
      ls -la;

   before_script:
    - apt -y update
    - apt install -y openssh-client
    - eval $(ssh-agent -s)
    - echo "$SERVER_SSH_KEY" | tr -d '\r' | ssh-add -
    - ls -la
    - mkdir -p ~/.ssh
    - chmod 700 ~/.ssh
    - ssh-keyscan $SERVER_IP >> ~/.ssh/known_hosts
    - chmod 644 ~/.ssh/known_hosts
#- echo $SERVER_SSH_KEY

   script:
     - echo 'V1 - commands in line'
     ############### ! Important 
     # For ssh to exit on error, start your commands with first command set -e 
     # - This will exit the executed on error with return - code > 0
     # - AND will throw an error from ssh and in pipeline  
     ###############
     - ssh root@$SERVER_IP -C "set -e; ls -la; cd $SERVER_WEBDIR; ls -la;"
     - echo 'V2 - content of Variable $CMD'
     - ssh root@$SERVER_IP -C $CMD
     - echo 'V3 - script locally - executed remotely'
     - ssh root@$SERVER_IP < good.sh
     - echo 'V4 - script in heredoc'
     - |
      ssh root@$SERVER_IP bash -s << HEREDOC
        echo "hello V4"
        ls -la
      HEREDOC
     - echo 'V5 - copy script and execute'
     - scp good.sh root@$SERVER_IP:/usr/local/bin/better.sh
     - ssh root@$SERVER_IP -C "chmod u+x /usr/local/bin/better.sh; better.sh"

```
