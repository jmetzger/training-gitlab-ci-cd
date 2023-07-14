# Gitlab CI/CD

## Agenda 

  1. gitlab ci/cd (Überblick)
     * [Architecture](/gitlab/architecture.md)
     * [Overview/Pipelines](/gitlab/01-ci-cd-overview.md)
     * [SaaS vs. On-Premise (Self Hosted)](gitlab/overview/saas-vs-on-premise.md)
     * [Jenkins mit Gitlab vs. gitlab ci/cd](gitlab/overview/jenkins-gitlab-vs-gitlab-cicd.md) 

  1. gitlab ci/cd (Praxis I) 
     * [Using the test - template](/gitlab/02-example-testtemplate.md)
     * [Examples running stages](/gitlab/03-example-running-stages.md) 
     * [Predefined Vars](/gitlab/04-predefined-vars.md)
     * [Variablen definieren](/gitlab/variables.md)
     * [Rules](/gitlab/05-rules.md)
     * [Example Defining and using artifacts](/gitlab/07-example-defining-and-using-artifacts.md)

  1. gitlab ci/cd (Praxis II)
     * [Mehrzeile Kommandos in gitlab ci-cd ausführen](/gitlab/jobs/script/multiline.md)
     * [Kommandos auf Zielsystem mit ssh ausführen (auch multiline)](gitlab/jobs/script/ssh-multiline.md)

  1. gitlab-ci/cd - Workflows
     * [Workflows + only start by starting pipeline](/gitlab/global/workflow.md)

  1. gitlab - ci/cd - Pipelines strukturieren / Templates 
     * [Includes mit untertemplates](gitlab/include/parent-child.md)
     * [Parent/Child Pipeline](/gitlab/parent-child-pipeline.md)
     * [Multiproject Pipeline / Downstream](/gitlab/multiproject-pipeline.md)
     * [Vorgefertigte Templates verwenden](gitlab/include/templates.md)
    
  1. gitlab - wann laufen jobs ? 
     * [Job nur händisch über Pipelines starten](gitlab/rules/only-web.md)
     * [Auch weiterlaufen, wenn Job fehlschlägt](gitlab/jobs/allow_failure.md)
    
  1. gitlab - setzen von Variablen
     * [Variablen für angepasste Builds verwenden und scheduled pipeline](gitlab/cases/variables-built-change.md)
    
  1. Exercises
     * [build with maven and using artifacts](https://github.com/jmetzger/training-gitlab-ci-cd/blob/main/gitlab/11-build-war-with-maven.md)
    
  1. gitlab ci/cd - docker
     * [Docker image automatisiert bauen - gitlab registry](/gitlab/09-use-gitlab-registry.md)
     * [Docker image automatisiert bauen - docker hub](/gitlab/09a-docker-build-use-docker-hub.md)
     * [Selbst gebauten Container manuell ausführen](/gitlab/docker/docker-image-manuell-ausfuehren.md)
     * [Neues Image in gitlab ci/cd aus gitlab registry verwenden](gitlab/global/default/image.md)

  1. Tipps&Tricks 
     * [Image/Container debuggen in mit gitlab ci/cd](gitlab/debug/container-kennenlernen.md)
     
  1. Documentation 
     * [gitlab ci/cd predefined variables](https://docs.gitlab.com/ee/ci/variables/predefined_variables.html)
     * [.gitlab-ci.yml Reference](https://docs.gitlab.com/ee/ci/yaml/)
     * [Referenz: global -> workflow](https://docs.gitlab.com/ee/ci/yaml/#workflow)
     * [Referenz: global -> default](https://docs.gitlab.com/ee/ci/yaml/#default)

  1. Documentation - Includes
     * [includes](https://docs.gitlab.com/ee/ci/yaml/includes.html)
     * [includes -> rules](https://docs.gitlab.com/ee/ci/yaml/includes.html#use-rules-with-include)
     * [includes -> rules -> variables](https://docs.gitlab.com/ee/ci/yaml/#rulesvariables)
     * [includes -> templates -> override-configuration](https://docs.gitlab.com/ee/ci/yaml/includes.html#override-included-configuration-values)
     * [includes -> defaults](https://docs.gitlab.com/ee/ci/yaml/includes.html#use-default-configuration-from-an-included-configuration-file)
    
  1. Documentation - Instances Limits
     * [applicaton limits](https://docs.gitlab.com/ee/administration/instance_limits.html)
     
## Backlog 

  1. Kubernetes (Refresher) 
     * [Aufbau von Kubernetes](kubernetes/architecture.md) 

  1. gitlab / Kubernetes CI/CD - old.old.schol with kubectl without agent)
     * [gitlab kubectl without agent](/gitlab/10-using-kubectl-old-style.md)

  1. gitlab / Kubernetes (gitops) 
     * [gitlab Kubernetes Agent with gitops - mode](/kubernetes-gitlab-gitops/example-gitlab-kubernetes-agent-with-gitops-mode.md)  
     
  1. gitlab / Kubernetes (CI/CD - old-school mit kubectl aber agent) 
     * [Vorteile gitlab-agent](/kubernetes/gitlab/advantage-gitlab-agent.md)
     * [Step 1: Installation gitlab-agent for kubernetes](/kubernetes-gitlab-ci-cd/99-gitlab-agent-with-kubectl.md)
     * [Step 2: Debugging KUBE_CONTEXT - Community Edition](kubernetes-gitlab-ci-cd/04-fix-problem-context-auto-devops.md)
     * [Step 3: gitlab-ci.yml setup for deployment and sample manifest](/kubernetes-gitlab-ci-cd/05-setup-deployment-with-sample-manifest.md)
     * [Documentation](https://docs.gitlab.com/ee/user/clusters/agent/ci_cd_workflow.html)

  1. gitlab / Kubernetes (CI/CD - Auto Devops) 
     * [Was ist Auto DevOps](/gitlab-ci-cd/was-ist-autodevops.md)
     * [Debugging KUBE_CONTEXT - Community Edition](kubernetes-gitlab-ci-cd/04-fix-problem-context-auto-devops.md)

  1. Tipps&Tricks
     * [Passwörter in Kubernetes verschlüsselt speichern](kubernetes/sealed-secrets.md)
  
