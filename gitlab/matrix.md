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

## Example 2

