# Den Container kennenlernen 

```
# in .gitlab-ci.yml
stages:          # List of stages for jobs, and their order of execution
  - build

build-job:       # This job runs in the build stage, which runs first.
  stage: build
  script:
    - echo "Compiling the code..."
    - echo "Compile complete."
    - cat /etc/os-release # Distribution Welche ? anzeigen 
    - pwd # aktuelle Verzeichnis, in dem ich bin ! # in welchem Verzeichnis bin ich  
    - ls -la # aktuelles verzeichnis in schöner "Admin" - Form 

```
