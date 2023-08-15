# gitlab before-script why ?

```
# Wir können einen hidden job definieren, der dann beim Job verwendet wird.
# Kommandos von before_script und script überschreiben sich nicht gegenseitig 


.install_dependencies:
  before_script:
    - pip install --upgrade pip
    - pip install -r requirements.txt 

my_test_job:
  extends: .install_dependencies 
  script:
     - pytest
```
