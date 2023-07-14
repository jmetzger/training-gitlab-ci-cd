# Container Scanning 

## Walkthrough 

```
include:
  - template: Security/Container-Scanning.gitlab-ci.yml

container_scanning:
  variables:
     CS_IMAGE: registry.gitlab.com/training.tn11/jochentest1:latest
```


## Ref:

  * https://docs.gitlab.com/ee/user/application_security/container_scanning/
