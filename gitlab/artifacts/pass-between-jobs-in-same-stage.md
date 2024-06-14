# Pass artifacts between jobs in same stage 

  * Important: needs keyword, so that they are NOT executed in parallel 

```
stages:          # List of stages for jobs, and their order of execution
  - build

build:
  stage: build
  script:
    - echo "in building..." >> ./control.txt
  artifacts:
    paths:
    - control.txt
    expire_in: 1 week


build-new:
  stage: build
  needs: ["build"]
  script:
    - ls -la
```
