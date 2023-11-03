# Container Scanning 

## Walkthrough (Variant 1)

```
include:
  - template: Security/Container-Scanning.gitlab-ci.yml

container_scanning:
  variables:
     CS_IMAGE: registry.gitlab.com/training.tn11/jochentest1:latest
```

## Walkthrough (Variant 2) - including building image 

```
include:
  - template: Jobs/Build.gitlab-ci.yml
  - template: Security/Container-Scanning.gitlab-ci.yml

container_scanning:
  variables:
    CS_DEFAULT_BRANCH_IMAGE: $CI_REGISTRY_IMAGE/$CI_DEFAULT_BRANCH:$CI_COMMIT_SHA
```


## Ref:

  * https://docs.gitlab.com/ee/user/application_security/container_scanning/
