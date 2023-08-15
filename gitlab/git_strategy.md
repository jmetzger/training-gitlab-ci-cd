# GIT_STRATEGY 

```
Es gibt tatsächlich ein GIT_DEPTH.
Zwei Probleme gibt es beim automatischen Clonen.
I. Es wird nur der aktuelle branch gezogen. 
II. Die Tiefe steht standardmäßig auf 20.
Das könnten man hochsetzen 


https://docs.gitlab.com/ee/ci/pipelines/settings.html#limit-the-number-of-changes-fetched-during-clone

Besser wäre wahrscheinlich 
GIT_STRATEGY none 
(bei den Variablen), dann greift nur das 2.)


Ausgabe, obwohl 2 Branches
 git branch -vr
  origin/main 5932a8c Update project1.gitlab-ci.yml


https://docs.gitlab.com/ee/ci/runners/configure_runners.html#git-fetch-extra-flags

variables:
  GIT_FETCH_EXTRA_FLAGS: --all
script:
  - ls -al cache/

---> RESULT: ated fresh repository.
fatal: fetch --all does not make sense with refspecs

So all does not work here, because we fetch a specific branch with refspec
```
