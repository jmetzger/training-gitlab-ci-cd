# kubectl (old style) 

```
https://sanderknape.com/2019/02/automated-deployments-kubernetes-gitlab/
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
