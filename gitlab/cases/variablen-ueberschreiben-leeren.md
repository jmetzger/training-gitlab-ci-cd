# Variablen überschreiben und unsetten 

## gitlab-ci.yml 

```
default:
  image: alpine


variables:
  VAR_GLOBAL: "meine globale var"

.base:
  script: test
  variables:
    VAR1: base var 1

job-test3:
  extends: .base
  variables: {} ## globale variable sollte danach eigentlich leer sein !! 
  script:
   - echo $VAR1
   - echo "global->"$VAR_GLOBAL

job-test4:
  extends: .base
  variables: null
  script:
  - echo $VAR1

```
