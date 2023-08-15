# docker compose project 

## Evolutions-Phase 2: Anwenden eines Docker Compose files über ssh 

### Schritt 1: gitlab-ci.yaml 

```
workflow:
  rules:
    - if: '$CI_PIPELINE_SOURCE == "web"'

default:
  image: alpine
stages:          # List of stages for jobs, and their order of execution
  - deploy 

deploy-job:
   stage: deploy   
   image: ubuntu 
  
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
    - cat $TOMCAT_SERVER_SSH_KEY >  ~/.ssh/id_rsa
    - chmod 600 ~/.ssh/id_rsa 

   script:
     - echo 'Deploying wordpres"
     - cd cms
     - export DOCKER_HOST=“ssh://root@$TOMCAT_SERVER_IP”
     - docker-compose up -d
```




```
docker compose up -d
```
