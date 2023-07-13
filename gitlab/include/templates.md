# Include Templates 

## Step 1: Browser Template in Pipeline Editor (Top-Bottom) to find the one you want

## Step 2: Include template in your gitlab-ci.yml - config

```

workflow:
  rules:
    - if: '$CI_PIPELINE_SOURCE == "web"'

stages:          # List of stages for jobs, and their order of execution
  - deploy 
  - test

include:
  template: Jobs/Test.gitlab-ci.yml

run-deploy:
  stage: deploy
  script:
    - echo "deploy started"


```
