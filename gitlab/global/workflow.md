# Workflows 

## What for ? 
  * Configure how pipelines behaves

## Only start pipeline by starting it with pipeline run (manually) 

```
# only: web geht hier nicht, aber das steht eigentlich für:
# '$CI_PIPELINE_SOURCE == "web"'
stages:
  - build 

workflow:
  rules:
    - if: '$CI_PIPELINE_SOURCE == "web"'

build-stage:
  stage: build  
  script: 
    - echo "hello build" 

```
