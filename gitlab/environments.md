# Environments 


```
1. In Operate -> Deployment  neues Environment Testing anlegen 
keine URL angeben - nur name 

2. In Settings->CI/CD-> Variables

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
