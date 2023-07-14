# Parent Child pipeline 

## gitlab-ci.yml 

```
project1:
  trigger:
    include: project1/project1.gitlab-ci.yml
    strategy: depend
  rules:
    - changes: [project1/*]
project2:
  trigger:
    include: project2/project2.gitlab-ci.yml
    strategy: depend
  rules:
    - changes: [project2/*]
```

## project1/project1.gitlab-ci.yml

```
stages:
  - build

project1.build-job:
  stage: build
  script:
    - echo "in project1 .. building"
    - echo $CI_PIPELINE_SOURCE
```

## project2/project2.gitlab-ci.yml

```
stages:
  - build

project2.build-job:
  stage: build
  script:
    - echo "in project2 .. building"
    - echo $CI_PIPELINE_SOURCE
```

