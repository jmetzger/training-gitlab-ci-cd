# Multiproject pipeline 

## Practical Example 

### Trigger - job in .gitlab-ci.yml 

```
trigger_job:
  trigger:
    project: training.tn11/jochentest-multi1 # project/repo sonst geht es nicht (muss komplett angegeben werden) 
    strategy: depend
```

### New repo -> training.tn11/jochentest-multi1 

```
# This is how my other project looks like 
workflow:
    rules:
      - if: '$CI_PIPELINE_SOURCE == "web"'
      - if: '$CI_PIPELINE_SOURCE == "pipeline"'

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

## Reference 

  * https://docs.gitlab.com/ee/ci/pipelines/downstream_pipelines.html?tab=Multi-project+pipeline
