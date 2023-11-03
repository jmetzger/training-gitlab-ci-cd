# Using a matrix to run multiple jobs concurrently 

## Example 1

```
stages:
  - build
  - test

build:
  stage: build
  script:
    - echo "Building $DISTRIBUTION on $ARCH"
  parallel:
    matrix:
      - DISTRIBUTION: [rhel8, ubuntu20]
        ARCH: [x64,x86]

test:
  stage: test
  script:
    - echo "Testing $DISTRIBUTION on $ARCH"
  parallel:
    matrix:
      - DISTRIBUTION: [rhel8, ubuntu20]
        ARCH: [x64,x86]
```

## Example 1a

```
stages:
  - build
  - test

.parallel-matrix:
  parallel:
    matrix:
      - DISTRIBUTION: [rhel8, ubuntu20]
        ARCH: [x64,x86]

build:
  stage: build
  extends: .parallel-matrix
  script:
    - echo "Building $DISTRIBUTION on $ARCH"
 

test:
  stage: test
  extends: .parallel-matrix
  script:
    - echo "Testing $DISTRIBUTION on $ARCH"
```

## Example 2

```
stages:
- matrix

.parallel-matrix:
  parallel:
    matrix:
      - CLOUD: 
        - aws
        - azure
        - gcp
        ARCH:
        - kubernetes
        - service-mesh

Matrix:
  stage: matrix
  image: alpine:latest
  extends: .parallel-matrix
  script:
  - echo "Hello from $ARCH from $CLOUD"

```


## Reference:

  * https://yashwanth-l.medium.com/gitlab-ci-parallel-with-matrix-7bd3acca8f70

