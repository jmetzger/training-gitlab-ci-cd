# Rollout docker-compose with scp and execute on remote

## Evolutions-Phase 3: 

### Schritt 1: docker-compose.yaml in gitlab anlegen 

```
# docker-compose.yaml
version: "3.8"

services:
  database:
    image: mysql:5.7
    volumes:
      - database_data:/var/lib/mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: mypassword
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: wordpress

  wordpress:
    image: wordpress:latest
    depends_on:
      - database
    ports:
      - 8080:80
    restart: always
    environment:
      WORDPRESS_DB_HOST: database:3306
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: wordpress
    volumes:
      - wordpress_plugins:/var/www/html/wp-content/plugins
      - wordpress_themes:/var/www/html/wp-content/themes
      - wordpress_uploads:/var/www/html/wp-content/uploads

volumes:
  database_data:
  wordpress_plugins:
  wordpress_themes:
  wordpress_uploads:
```

### Schritt 2: gitlab-ci.yaml 

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
    - apt-get -y update
    - apt-get install -y openssh-client 
    - eval $(ssh-agent -s)
    - echo "$TOMCAT_SERVER_SSH_KEY" | tr -d '\r' | ssh-add -
    - ls -la
    - mkdir -p ~/.ssh
    - chmod 700 ~/.ssh
    - ssh-keyscan $TOMCAT_SERVER_IP >> ~/.ssh/known_hosts
    - chmod 644 ~/.ssh/known_hosts
    - echo $TOMCAT_SERVER_SSH_KEY
    # eventually not neededrsa 

   script:
     - echo 'Deploying wordpress'

     - |
       ssh root@$TOMCAT_SERVER_IP bash -s << HEREDOC
        cd
        mkdir -p cms 
       HEREDOC 
     - scp cms/docker-compose.yaml root@$TOMCAT_SERVER_IP:~/cms/
     - ssh root@$TOMCAT_SERVER_IP -C "cd; cd cms; docker compose up -d"

```

