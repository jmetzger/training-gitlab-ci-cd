# Build war-file with maven 

## Part 1: pom.xml  (Project Object Model)

```
# put this file:
pom.xml
# in top folder
```

```
<project xmlns="http://maven.apache.org/POM/4.0.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>io.happycoding</groupId>
  <artifactId>hello-world-maven</artifactId>
  <version>1</version>
  <packaging>war</packaging>

  <properties>
    <!-- Java 11 -->
    <maven.compiler.source>11</maven.compiler.source>
    <maven.compiler.target>11</maven.compiler.target>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  </properties>

  <dependencies>
    <!-- Jakarta Servlets API -->
    <dependency>
      <groupId>jakarta.servlet</groupId>
      <artifactId>jakarta.servlet-api</artifactId>
      <version>5.0.0</version>
      <scope>provided</scope>
    </dependency>
  </dependencies>

  <build>
    <plugins>
      <!-- Enable building as a .war file with `mvn package` -->
      <plugin>
        <artifactId>maven-war-plugin</artifactId>
        <version>3.3.1</version>
      </plugin>
    </plugins>

    <!-- The output .war file's name, which will be the name of the webapp. -->
    <finalName>${project.artifactId}</finalName>
  </build>
</project>
```

## Part 2:  src/main/webapp/index.html 
```
<!DOCTYPE html>
<html>
  <head>
    <title>Server Hello World: Maven</title>
  </head>
  <body>
    <h1>Happy Coding</h1>
    <p>Hello world!</p>
  </body>
</html>
```

## Part 3: src/main/java/io/happycoding/servlets/HelloWorldServlet.java

```
package io.happycoding.servlets;

import java.io.IOException;

import jakarta.servlet.annotation.WebServlet;
import jakarta.servlet.http.HttpServlet;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;

@WebServlet("/hello")
public class HelloWorldServlet extends HttpServlet {

  @Override
  public void doGet(HttpServletRequest request, HttpServletResponse response)
      throws IOException {
    response.setContentType("text/html;");
    response.getWriter().println("<h1>Hello world!</h1>");
  }
}
```

## Part 4: .gitlab-ci.yml 

```
# create
.gitlab-ci.yml
# file
```

```
image: maven:latest

stages:          # List of stages for jobs, and their order of execution
  - build

build-job:       # This job runs in the build stage, which runs first.
  stage: build
  script:
    - ls -la
    - mvn package
    - ls -la
    - cd target
    - ls -la
```

## Optional Part 4a: Also create artifact 

```
image: maven:latest

variables:
  PROJECT_ARTIFACTS_ID: roadrunner
  

stages:          # List of stages for jobs, and their order of execution
  - build

build-job:       # This job runs in the build stage, which runs first.
  stage: build
#  only:
#    - web
  script:
    - mvn package
    - ls -la
    - cd target
    - ls -la
  artifacts:
   paths:
      - target/$PROJECT_ARTIFACTS_ID.war # no '$VAR' or "$VAR" here, it does not work
```

## Optional Part 4b: Artifacts with wildcard 

```
image: maven:latest

stages:          # List of stages for jobs, and their order of execution
  - build

build-job:       # This job runs in the build stage, which runs first.
  stage: build
#  only:
#    - web
  script:
    - mvn package
    - ls -la
    - cd target
    - ls -la
  artifacts:
   paths:
      - target/*.war # no '$VAR' or "$VAR" here, it does not work
                     # All war-files shall be artifacts 
```

## Optional Part 4c: Increasing performance, but not doing git checkout

```

default:
  image: maven:latest

stages:          # List of stages for jobs, and their order of execution
  - build
  - deploy

build-job:       # This job runs in the build stage, which runs first.
  stage: build
#  only:
#    - web
  script:
    - mvn package
    - ls -la
    - cd target
    - ls -la
  artifacts:
   paths:
      - target/*.war # no '$VAR' or "$VAR" here, it does not work
                     # All war-files shall be artifacts 

deploy-job:
  stage: deploy
  variables:
    GIT_STRATEGY: none
  image: busybox 
  script:
    - echo "hello deployment"
    - ls -la

```

## Uploading it to tomcat - server 

### 1. Todos beforehand 

  * Setup tomcat - server
  * Create a public private  - key for root or user that can access tomcat folder
  * Which directory ?:
    * /var/lib/tomcat9/webapps
  * Which server ?:
    * e.g. 

##### 2. On tomcat machine 

```
# id -> root
ssh-keygen -t rsa
```

##### 3. in gitlab -> project 

```
# Set variables under
Settings -> CI/CD -> Variables
(Do not protect them)

# Fill it with with data from tomcat

TOMCAT_SERVER_IP
# This will be the private key, we created
# content of /root/.ssh/id_rsa
TOMCAT_SERVER_SSH_KEY
TOMCAT_SERVER_WEBDIR
```

##### 4. Change deploy - job as follows 

```
deploy-job:
  stage: deploy
  variables:
    GIT_STRATEGY: none

  script:
    - echo "hello deployment"
    - ls -la

deploy-job:
  image: ubuntu
  stage: deploy
  variables:
    GIT_STRATEGY: none

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
     - scp -o StrictHostKeyChecking=no target/*.war root@$TOMCAT_SERVER_IP:$TOMCAT_SERVER_WEBDIR
     - cd $TOMCAT_SERVER_WEBDIR
     - ls -la

```




