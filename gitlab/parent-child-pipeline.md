# Parent Child pipeline 

## Variante 1: gitlab-ci.yml (no subfolders) 

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

## Variante 2: gitlab-ci.yml (with subfolders) 

```
project1:
  trigger:
    include: project1/project1.gitlab-ci.yml
    strategy: depend
  rules:
    - changes: [project1/**/*]
project2:
  trigger:
    include: project2/project2.gitlab-ci.yml
    strategy: depend
  rules:
    - changes: [project2/**/*]
```

## Variante 3: gitlab-ci.yml (with subfolders ....) 

  * Not able to be started on run pipeline (manually)
  * But, when it is triggered on changes

```
workflow:
  rules:
    - if: '$CI_PIPELINE_SOURCE == "web"'
      when: never
    - when: always

project1:
  trigger:
    include: project1/project1.gitlab-ci.yml
    strategy: depend
  rules:
    - changes: [project1/**/*]
project2:
  trigger:
    include: project2/project2.gitlab-ci.yml
    strategy: depend
  rules:
    - changes: [project2/**/*]
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

## Alternative mit anderen stages in child 

```
stages:
  - project1-build
  - project1-test
  - project1-deploy 


project1.build-job:
  stage: project1-build
  script:
    - echo "in project1 .. building"
    - echo $CI_PIPELINE_SOURCE

project1.test-job:
  stage: project1-test
  script:
    - echo "in project1 .. test"
    - echo $CI_PIPELINE_SOURCE

project1.deploy-job:
  stage: project1-deploy
  script:
    - echo "in project1 .. deploy"
    - echo $CI_PIPELINE_SOURCE
```



## Refs:

  * https://docs.gitlab.com/ee/ci/pipelines/downstream_pipelines.html
