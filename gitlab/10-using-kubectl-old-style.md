# kubectl (old style without agent) 

## Walkthrough 

```
1. Create new repo on gitlab 
2. CI/CD workflow aktivieren, in dem wir auf das Menü CI/CD klicken 
-> Get started with GitLab CI/CD -> Use Template 

3. file .gitlab-ci.yml anpassen

```


```
variables:
   KUBECONFIG_SECRET: $KUBECONFIG_SECRET

build-version:       # This job runs in the build stage, which runs first.
  stage: build
  image: 
#    name: dtzar/helm-kubectl:3.7.1
    name: bitnami/kubectl:latest
    entrypoint: [""]
  script:
    - echo "Show use our repo"
    - cd $CI_PROJECT_DIR
    - ls -la
    - kubectl version --client
    - echo "kubeconfig aufsetzen"
    - mkdir -p ~/.kube
    - echo "$KUBECONFIG_SECRET" > ~/.kube/config
    - ls -la ~/.kube/config
    - cat ~/.kube/config
    - kubectl cluster-info 
    - kubectl get pods
    - echo "Deploying..."
# - kubectl apply -f manifests/deploy.yml
    - sleep 2
    - echo "And now..."
    - kubectl get pods 
```


```
# manifests anlegen in manifests/01-deploy.yml 
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 2 # tells deployment to run 2 pods matching the template
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80        
```


```
4. Zugangsdaten auf master-server auslesen und in den Zwischenspeicher kopieren

microk8s config

5. Im Repo und SETTINGS -> CI/CD -> Variables 

variable 
KUBECONFIG_SECRET 
mit Inhalt aus 4. setzen

MASKED und PROTECTED Nicht aktivieren 

Speicern

6. im repo folgende Datei anlegen. 

# manifests/deploy.yml 
apiVersion: apps/v1
kind: Deployment
metadata:
  name: echo-server-deployment-from-gitlab
  labels:
    app: echo-server
spec:
  selector: 
    matchLabels:  
      app: echo-server 
  replicas: 1
  template:
    metadata:
      annotations:
      labels:
        app: echo-server
    spec:
      containers:
        - name: echo-server
          image: hashicorp/http-echo
          imagePullPolicy: IfNotPresent
          args:
            - -listen=:8080
            - -text="hello NEWNEW world"


7. in CI/CD - Menü -> Pipelines gucken, ob die Pipeline durchläuft und die detaillierte Ausgabe anzeigen

8. Änderung in deploy.yml durchführen.

z.B. Text: hello NEWNEW world in hello OLDNEW world ändern. 

9. Prüfen ob neuer Pod erstellt wird durch überprüfen der Ausgabe in Pipelines 

```



```
deploy:
  image:
    name: bitnami/kubectl:latest
    entrypoint: ['']
  script:
    - kubectl config get-contexts
    - kubectl config use-context path/to/agent/repository:agent-name
    - kubectl get pods
```


## A bit nicer: 

```
https://sanderknape.com/2019/02/automated-deployments-kubernetes-gitlab/
```
