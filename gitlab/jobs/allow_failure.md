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
    - sleep 120

build_job3:
   stage: build
   script:
     - echo "ich bin job3" 

deploy_job:
  stage: deploy
  script: 
    - echo "i am good to go"
    - sleep 30

```
