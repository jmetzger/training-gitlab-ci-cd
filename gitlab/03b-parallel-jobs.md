# Examples running stages (parallel jobs) 



## Show they run parallel 

```
# einfaches stages - keyword ergänzen und die stages die man haben will 
stages:
  - build
  - deploy


build-job:       # This job runs in the build stage, which runs first.
  stage: build
  script:
    - sleep 120
    - echo "after 120 seconds -> Compiling the code..."
    - echo "Compile complete."

build-job2:
  stage: build
  script:
    - echo "ready even ealier ? now also done"  

deploy-job:      # This job runs in the deploy stage.
  stage: deploy  # It only runs when *both* jobs in the test stage complete successfully.
  script:
    - echo "Deploying application..."
    - echo "Application successfully deployed."


```

 * Danach sich die Pipelines anschauen (CI/CD -> Pipeline) 
