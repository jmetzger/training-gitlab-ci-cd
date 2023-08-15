# Multiproject pipeline 

## Practical Example 

### Trigger - job in .gitlab-ci.yml 

```
trigger_job:
  trigger:
    project: training.tn1/jochentest-multi1 # project/repo sonst geht es nicht (muss komplett angegeben werden) 
    strategy: depend
```

### New repo -> training.tn1/jochentest-multi1 

```
# This is how my other project looks like 
workflow:
    rules:
      - if: '$CI_PIPELINE_SOURCE == "web"'
      - if: '$CI_PIPELINE_SOURCE == "pipeline"' # ein projekt gestart innerhalb multiproject - pipeline 

default:
  image: alpine

stages:          # List of stages for jobs, and their order of execution
  - build
  
build-job:       # This job runs in the build stage, which runs first.
  stage: build
  script:
    - echo "Started"
    - echo "Show us the pipeline source $CI_PIPELINE_SOURCE"
```

## Version 1: Deploy after all Build triggers are done 

```
stages:
  - build
  - deploy

project1:
  stage: build
  trigger:
    include: project1/project1.gitlab-ci.yml
    strategy: depend
 # rules:
 #   - changes: [project1/**/*]
project2:
  stage: build
  trigger:
    include: project2/project2.gitlab-ci.yml
    strategy: depend
  rules:
    - changes: [project2/**/*]

trigger_job:
  stage: build
  trigger:
    project: training.tn11/jochentest-multi2 # project/repo sonst geht es nicht (muss komplett angegeben werden) 
    strategy: depend

deploy_job:
  stage: deploy
  image: alpine
  script: 
    - echo "i am good to go"
    - sleep 30

```


## Reference 

  * https://docs.gitlab.com/ee/ci/pipelines/downstream_pipelines.html?tab=Multi-project+pipeline
