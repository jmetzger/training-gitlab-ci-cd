# extend and anchor 

## Hinweis:

 * Dinge, die wiederverwendet werden sollen, müssen vorher definiert sein, in der Datei
 * d.h. .base vor myjob
 * .default_scripts bzw &default_scripts vor Verwendung als *default_scripts 

## gitlab-ci.yml 

```
.base:
  variables:
    TEST_CASE: "true"
    VERSION: "1.0"

.default_scripts: &default_scripts
  - echo "from _default_scripts"
  - echo "next default step"

myjob:
  variables:
    TEST_CASE: 'bad'
  extends: .base
  script: 
    - *default_scripts
    - echo "in MYJOB"
    - ls -la
    - echo $TEST_CASE
    - echo $VERSION

```

