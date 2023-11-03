# Environments 

## Variant 1: Add Environment in Operate -> Environments

```
1. In Operate -> Deployment  neues Environment Testing anlegen 
keine URL angeben - nur name 

2. In Project -> Settings->CI/CD-> Variables

Variable 1:
CODE_BRANCH   testing   (Environment: Testing) 
CODE_BRANCH   main      (Environment: Production) 

3. Kleines Code-Schnipsel 
(normalerweise wird es in deploy verwenden 
und hat dort noch Zusatzintegrationen)
```

```
stages:
  - build


build-prod:
    stage: build
    environment:
        name: production
        action: prepare
    script:
       echo "That is the code branch "$CODE_BRANCH 

build-testing:
    stage: build
    environment:
        name: testing
        action: prepare
    script:
       echo "That is the code branch "$CODE_BRANCH

```

## Variant 2: Add environment statically through gitlab-ci.yaml 

```
# add enviroment to .gitlab-ci.yaml
stages:
  - deploy

deploy_staging:
  stage: deploy
  script:
    - echo "deploy to staging"
    - echo "$CODE_BRANCH"
  environment:
     name: staging
  when: manual

deploy_production:
  stage: deploy
  script:
    - echo "deploy to production"
    - echo "$CODE_BRANCH"
  environment:
     name: production
  when: manual
```

```
# Start pipeline - if not already done after saving
```

```
# Now enter 2 variables in Settings -> CI/CD Variables
For CODE_BRANCH / production
For CODE_BRANCH / staging 
```

![image](https://github.com/jmetzger/training-gitlab-ci-cd/assets/1933318/db608b3d-22f3-4fd0-b1ec-666a38b24032)

```
# Start jobs manually in pipeline
# and watch log for CODE_BRANCH
```

![image](https://github.com/jmetzger/training-gitlab-ci-cd/assets/1933318/c8c4dcb4-78c3-4a3c-90d8-3bce36c2dce4)

