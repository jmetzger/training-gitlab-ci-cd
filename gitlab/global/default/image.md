# Alternatives image verwenden aus registry 

## gitlab-ci.yml 

```
stages:          # List of stages for jobs, and their order of execution
  - build


build-new:
  stage: build
  image: registry.gitlab.com/training.tn11/jochentest1
  script:
    - which ssh
```

## Ausführen und glücklich sein ! 
