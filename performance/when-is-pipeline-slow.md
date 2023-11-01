# Wann ist eine Pipeline langsam 

## Repo ist sehr gross

  * was kann ich tun: depth niedriger setzen, statt 20
  * Brauche ich das Repo in dem Job ?-> ansonsten GIT_STRATEGY: none 

## Image ist zu gross 

  * Image verschlanken, wenn es keine Standard-Image ist, im Image-Bauprozes

## Caching 

  * Wenn caching verwendet und wenn ja richtig ?

## Scheduling in der Pipelines 

  * sehr lange Laufzeiten, weil einzelne Stages sehr lange brauchen (standardverhalten: jeder Stage muss komplett fertig sein, damit der nächste Stage starten kann)
  * Lösung: Acyclice Pipelines: z.B. build_a -> test_a -> deploy_a kann parallel laufen zu build_b -> test_b -> deploy_b

## Job abspecken / zu langsam 

  * Muss ich wirklich alles in diesem Job so machen oder kann ich Sachen weglassen (weil redundant, nicht notwendig)

## Brauche ich artifakte in jedem Job, ansonsten deaktivieren

```
# only change in stage: build 
image: ubuntu:20.04

# stages are set to build, test, deploy by default 

build:
  stage: build
  script:
    - echo "in building..." >> ./control.txt
  artifacts:
    paths:
    - control.txt
    expire_in: 1 week

my_unit_test:
  stage: test
  dependencies: []
  script:
    - ls -la 
    - echo "no control.txt here"
    - ls -la 

deploy:
  stage: deploy
  script:
    - ls
    - cat control.txt
```
