# Rollout docker-compose with scp and execute on remote

## Evolutions-Phase 3: 

### Vorbereitung: 

  * SSH_SERVER_KEY (private key), SERVER_IP als Variablen in Settings -> CI/CD angelegt werden. 

### Schritt 1: cms/docker-compose.yaml in gitlab anlegen 

```
services:
  db:
    # We use a mariadb image which supports both amd64 & arm64 architecture
    image: mariadb:10.6.4-focal
    command: '--default-authentication-plugin=mysql_native_password'
    volumes:
      - db_data:/var/lib/mysql
    restart: always
    environment:
      - MYSQL_ROOT_PASSWORD=somewordpress
      - MYSQL_DATABASE=wordpress
      - MYSQL_USER=wordpress
      - MYSQL_PASSWORD=wordpress
    expose:
      - 3306
      - 33060
  wordpress:
    image: wordpress:latest
    volumes:
      - wp_data:/var/www/html
    ports:
      - 80:80
    restart: always
    environment:
      - WORDPRESS_DB_HOST=db
      - WORDPRESS_DB_USER=wordpress
      - WORDPRESS_DB_PASSWORD=wordpress
      - WORDPRESS_DB_NAME=wordpress
volumes:
  db_data:
  wp_data:
```

### Schritt 2: gitlab-ci.yaml 

```
workflow:
  rules:
    - if: '$CI_PIPELINE_SOURCE == "web"'

stages:          # List of stages for jobs, and their order of execution
  - deploy 

deploy-job:
   stage: deploy   
   image: ubuntu 
  
   before_script:
    - apt-get -y update
    - apt-get install -y openssh-client 
    - eval $(ssh-agent -s)
    - echo "$SERVER_SSH_KEY" | tr -d '\r' | ssh-add -
    - mkdir -p ~/.ssh
    - chmod 700 ~/.ssh
    - ssh-keyscan $SERVER_IP >> ~/.ssh/known_hosts
    - chmod 644 ~/.ssh/known_hosts
    #- echo $SERVER_SSH_KEY
    # eventually not neededrsa 

   script:
     - echo 'Deploying wordpress'

     - |
       ssh root@$SERVER_IP bash -s << HEREDOC
        cd
        mkdir -p cms 
       HEREDOC 
     - scp cms/docker-compose.yaml root@$SERVER_IP:~/cms/
     - ssh root@$SERVER_IP -C "cd; cd cms; docker compose up -d"

```

### Schritt 3: Pipeline manuell über pipeline menü starten 
