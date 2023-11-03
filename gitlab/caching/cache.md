# Cache 

## Key facts 

  * Caches are reused in pipelines
  * Use to cache depenedencies (libraries a.s.o)
  * Use artifacts, if data is created by a job
  * the cache is stored in the same place where GitLab Runner is installed. If the distributed cache is configured, S3 works as storage.

## Example 

### Prepare 

  * Import this repo: https://gitlab.com/gitlab-examples/nodejs.git

### Iteration 1: Use a cache 

```
image: node:latest # (1)

# This folder is cached between builds
cache:
  paths:
    - node_modules/ # (2)

test_async:
  script:
    - npm install # (3)
    - node ./specs/start.js ./specs/async.spec.js

test_db:
  script:
    - npm install # (4)
    - node ./specs/start.js ./specs/db-postgres.spec.js

```

### Iteration 2: Modify .gitlab-ci.yaml 

```
image: node:16.3.0 # (1)

stages:
  - setup
  - test

variables:
  npm_config_cache: "$CI_PROJECT_DIR/.npm"

# Define a hidden job to be used with extends
# Better than default to avoid activating cache for all jobs
.dependencies_cache:
  cache:
    key:
      files:
        - package-lock.json
    paths:
      - .npm
    policy: pull

setup:
  stage: setup
  script:
    - npm install
  extends: .dependencies_cache
  cache:
    policy: pull-push
  artifacts:
    expire_in: 1h
    paths:
      - node_modules

test_async:
  stage: test
  script:
    - node ./specs/start.js ./specs/async.spec.js

test_db:
  stage: test
  script:
    - node ./specs/start.js ./specs/db-postgres.spec.js
```

### Iteration 3: Modify .gitlab-ci.yaml 

  * package-lock.json bauen (npm install) und als artifact zur Verfügung stellen 

```
image: node:16.3.0 # (1)

stages:
  - setup
  - test

variables:
  npm_config_cache: "$CI_PROJECT_DIR/.npm"

# Define a hidden job to be used with extends
# Better than default to avoid activating cache for all jobs
.dependencies_cache:
  cache:
    key:
      files:
        - package-lock.json
    paths:
      - .npm
    policy: pull

setup:
  stage: setup
  script:
    - npm install
  extends: .dependencies_cache
  cache:
    policy: pull-push
  artifacts:
    expire_in: 1h
    paths:
      - node_modules
      - package-lock.json

test_async:
  stage: test
  script:
    - node ./specs/start.js ./specs/async.spec.js

test_db:
  stage: test
  script:
    - node ./specs/start.js ./specs/db-postgres.spec.js
```

```
# Artifact runterladen, Inhalt aus package-lock.json rauskopieren und Datei in Repo erstellen
# package-lock.json und Inhalt einfügen
```




### Reference:

  * https://dev.to/drakulavich/gitlab-ci-cache-and-artifacts-explained-by-example-2opi
