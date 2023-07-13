# Use gitlab - registry

## Dockerfile - RootLevel 

```
FROM ubuntu:latest
# 
RUN  apt-get update && \
     apt-get install -y openssh-client  
COPY good.sh /usr/local/bin/better.sh
```

## .gitlab-ci.yml 

```
stages:          # List of stages for jobs, and their order of execution
  - build

build-image:       # This job runs in the build stage, which runs first.
  stage: build
  image: docker:20.10.10
  services:
     - docker:20.10.10-dind
  script:
    - echo "user:"$CI_REGISTRY_USER
    - echo "pass:"$CI_REGISTRY_PASSWORD
    - echo "registry:"$CI_REGISTRY
    - echo $CI_REGISTRY_PASSWORD | docker login -u $CI_REGISTRY_USER $CI_REGISTRY --password-stdin
    - docker build -t $CI_REGISTRY_IMAGE .
    - docker images
    - docker push $CI_REGISTRY_IMAGE
    - echo "BUILD for $CI_REGISTRY_IMAGE done"
```
