# Cache 

## Key facts 

  * Caches are reused in pipelines
  * Use to cache depenedencies (libraries a.s.o)
  * Use artifacts, if data is created by a job
  * the cache is stored in the same place where GitLab Runner is installed. If the distributed cache is configured, S3 works as storage.

## Example 

### Prepare 

  * Import this repo: https://gitlab.com/gitlab-examples/nodejs/-/blob/master/.gitlab-ci.yml

### Modify .gitlab-ci.yaml 

```
image: node: 16.3.0 # (1)

stages:
  - test

variables:
  npm_config_cache: "$CI_PROJECT_DIR/.npm" (5)

# This folder is cached between builds
cache:
  key:
    files:
      - package-lock.json (6)
  paths:
    - .npm # (2)

test_async:
  stage: test
  script:
    - npm ci # (3)
    - node ./specs/start.js ./specs/async.spec.js

test_db:
  stage: test
  script:
    - npm ci # (4)
    - node ./specs/start.js ./specs/db-postgres.spec.js
```


### Reference:

  * https://dev.to/drakulavich/gitlab-ci-cache-and-artifacts-explained-by-example-2opi
