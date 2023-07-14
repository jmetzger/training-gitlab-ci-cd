# Jobs on-failure 

## Walkthrough 

```
stages:
  - build
  - deploy

default:
  image: alpine 

build_job1:
  stage: build 
  allow_failure: true
  script:
    - xls 

build_job2:
  stage: build
  script:
    - ls -la 

deploy_job:
  stage: deploy
  script: 
    - echo "i am good to go"
    - sleep 30

```
