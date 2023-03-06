# Tekton-pipeline
## Objetivo:
Este projeto tem como objetivo a criação de um projeto simples para implementação de uma pipeline com Tekton-pipelines. Ela possui as tarefas de clonar o código fonte do repositório, fazer o build da imagem e efetuar um push para um repositório no DockerHub.

## Requisitos

    - Cluster de Kubernetes;
    - Noções de programação;
___    
## Execução:
### Instale o tekton-pipelines

    kubectl apply --filename https://storage.googleapis.com/tekton-releases/pipeline/latest/release.yaml

### Instale tekton-dashboard

    kubectl apply --filename https://storage.googleapis.com/tekton-releases/dashboard/latest/release.yaml

Faça o port-forward do dashboard tekton:

    kubectl port-forward svc/tekton-dashboard 9097 -n tekton-pipelines

### Instale tekton-triggers

    kubectl apply --filename https://storage.googleapis.com/tekton-releases/triggers/latest/release.yaml

### Instale os Interceptors

    kubectl apply --filename https://storage.googleapis.com/tekton-releases/triggers/latest/interceptors.yaml

### Instale as Tasks:

#### Git-Clone:

    kubectl apply -f https://raw.githubusercontent.com/tektoncd/catalog/main/task/git-clone/0.6/git-clone.yaml

#### Kaniko:

    kubectl apply -f https://raw.githubusercontent.com/tektoncd/catalog/main/task/kaniko/0.6/kaniko.yaml

