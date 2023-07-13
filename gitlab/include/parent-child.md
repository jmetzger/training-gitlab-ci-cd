# Create parent-child project

## Prerequisites 

```
1x main .gitlab-ci.yml

1x project1/project1.gitlab-ci.yml
1x project2/project2.gitlab-ci.yml
```

## Step 1a: gitlab-ci.yml (simple)

```
stages:          # List of stages for jobs, and their order of execution
  - build

include:
   - project1/project1.gitlab-ci.yml
   - project2/project2.gitlab-ci.yml


```

## Step 1b: gitlab-ci.yml (start with pipeline start and variable setting

```
workflow:
  rules:
    - if: '$CI_PIPELINE_SOURCE == "web"'

stages:          # List of stages for jobs, and their order of execution
  - build

include:
 
include:
   - local: project1/project1.gitlab-ci.yml
     rules:
       - if: $BUILD_PROJECT1 == "true"

   - local: project2/project2.gitlab-ci.yml
     rules:
       - if: $BUILD_PROJECT2 == "true"

dummy-build:
   stage: build
   script:
     - echo "dummy build"
   rules:
     - if: $BUILD_PROJECT1 == "true" || $BUILD_PROJECT2 == "true"
       when: never

```


## Step 2: project1/project1.gitlab-ci.yml 

```
stages:
  - build

project1.build-job:
  stage: build
  script:
    - echo "in project1 .. building"

```

## Step 3: project2/project2.gitlab-ci.yml 

```
stages:
  - build

project2.build-job:
  stage: build
  script:
    - echo "in project2 .. building"
```
