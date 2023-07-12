# Variablen definieren 

## Möglichkeit 1: TopLevel (Im Project) 

```
# Settings -> CI/CD -> Variables
```

## Beispiele:

```
# gitlab-ci.yml
variables:
  TEST_URL: http://schulung.t3isp.de # globalen Scope - in der gesamten Pipeline
                                     # Überschreibt NICHT -> ... Settings -> CI/CD -> Variables   
  TEST_VERSION: "1.0" # global 
  TEST_ENV: Prod # global 

stages:
  - build 
  - test
  
show_env:
  stage: build 

  variables:
    TEST_JOB: lowrunner # variable mit lokalem Scope - nur in Job 
    TEST_URL: http://www.test.de # Auch das überschreibt NICHT -> ... Settings -> CI/CD -> Variables 

  script:
  - echo $TEST_URL
  - echo $TEST_URL > /tmp/urltest.txt
  - cat /tmp/urltest.txt
  - echo $TEST_CONTENT # tolle Sache
  - cat $TEST_CONTENT
  - echo $TEST_VERSION
  - echo $TEST_ENV
  - echo $TEST_JOB

test_env:
  stage: test 

  script:
  - echo $TEST_URL
  - echo $TEST_CONTENT # tolle Sache
  - cat $TEST_CONTENT
  - echo $TEST_VERSION
  - echo $TEST_ENV
  - echo $TEST_JOB







```

## Reihenfolge, welche Variablen welche überschreien (Ebenene) 

  * https://docs.gitlab.com/ee/ci/variables/#cicd-variable-precedence
