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
    - echo $PATH
```

## Ausführen und glücklich sein ! 


## Einloggen mit Docker Credentials 

```
echo -n "username:access-token" | base64 

DOCKER_AUTH_CONFIG

"auths": {
  "registry.gitlab.com": {
    "auth": "LSBuIHRyYWluaW5nMTE6Z2xwYXQtTlpILXNTNXhtNEZBeFdTekpBZnkK"
  }
}

```

```
Eintragen von DOCKER_AUTH_CONFIG -> in Settings -> CI/CD -> Variables
```

## Refs:

  * https://mherman.org/blog/gitlab-ci-private-docker-registry/
