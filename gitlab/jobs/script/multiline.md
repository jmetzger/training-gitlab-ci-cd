# Multiline Scripts in gitlab ci/cd 

## Step 1: 

 * Create new repo

## Step 2: create good.sh next to README.md

  * Create file good.sh in repo root-level 

```
#!/bin/bash

echo "good things start now"
ls -la
date
```

## Step 3: create gitlab-ci.yml with Pipeline Editor 

```
stages:
  - build 

workflow:
  rules:
  - if: $CI_PIPELINE_SOURCE == "web"

build-stage:
  stage: build
  variables:
    CMD: |
      echo hello-you; 
      ls -la;
  script: 
  - echo "execute script from git repo"
  - bash -s < good.sh
  - echo -n $CMD
  - echo "eval the command"
  - bash -c "$CMD"
  - |-
      bash -s << HEREDOC
        echo hello 
        ls -la
      HEREDOC
  - |
      tr a-z A-Z << END_TEXT
        one two three
        four five six
      END_TEXT 
  - |
      bash -s << HEREDOC
        echo hello 
        ls -la
      HEREDOC
  - |-
      tr a-z A-Z << END_TEXT
        one two three
        four five six
      END_TEXT
  - >
      echo "First command line
      is split over two lines."

      echo "Second command line."
 

```

## Run Pipeline (need to trigger manually) 



## Reference 


## Reference:

  * https://docs.gitlab.com/ee/ci/yaml/script.html#split-long-commands
  * https://stackoverflow.com/questions/3790454/how-do-i-break-a-string-in-yaml-over-multiple-lines/21699210#21699210
   

  * https://docs.gitlab.com/ee/ci/yaml/script.html#split-long-commands
