# Create parent-child project

## Prerequisites 

```
1x main .gitlab-ci.yml

1x project1/project1.gitlab-ci.yml
1x project2/project2.gitlab-ci.yml
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
