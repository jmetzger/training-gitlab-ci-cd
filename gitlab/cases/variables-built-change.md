# Use different settings for variables for built

## gitlab-ci.yml 

```
workflow: 
  rules:
    - if: $CI_PIPELINE_SOURCE == "web"

image: alpine
# correct: eigenes image oder maven 

stages:
  - build

job-from-scheduler:
  stage: build
  
  rules:
    - if: $CRON_BUILD_TYPE == "snapshot"
      variables:                              # Override DEPLOY_VARIABLE defined
        MVN_BUILD_GOAL: "snapshot"  # at the job level.
    - if: $CRON_BUILD_TYPE == "release"
      variables:
        MVN_BUILD_GOAL: "release"                 # Define a new variable.
  script:
    - echo "Run script with $DEPLOY_VARIABLE as an argument"
    - echo "Run another script if $IS_A_FEATURE exists"
    - echo "mvn $MVN_BUILD_GOAL"
```
