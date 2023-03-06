# Tekton-pipeline
## Objetivo:
Este projeto tem como objetivo a criação de um projeto simples para implementação de uma pipeline com Tekton-pipelines. Ela possui as tarefas de clonar o código fonte do repositório, fazer o build da imagem e efetuar um push para um repositório no DockerHub.

## Requisitos

    - Cluster de Kubernetes;
    - Noções de programação;
    - Feramenta kubectl;
___    
## Execução:
### Instale o tekton-pipelines

    kubectl apply --filename https://storage.googleapis.com/tekton-releases/pipeline/latest/release.yaml

### Instale tekton-dashboard

    kubectl apply --filename https://storage.googleapis.com/tekton-releases/dashboard/latest/release.yaml

Faça o port-forward do dashboard tekton:

    kubectl port-forward svc/tekton-dashboard 9097 -n tekton-pipelines

___
### Instale tekton-triggers

    kubectl apply --filename https://storage.googleapis.com/tekton-releases/triggers/latest/release.yaml

### Instale os Interceptors

    kubectl apply --filename https://storage.googleapis.com/tekton-releases/triggers/latest/interceptors.yaml

___
### Instale as Tasks:
#### Git-Clone:

    kubectl apply -f https://raw.githubusercontent.com/tektoncd/catalog/main/task/git-clone/0.6/git-clone.yaml

#### Kaniko:

    kubectl apply -f https://raw.githubusercontent.com/tektoncd/catalog/main/task/kaniko/0.6/kaniko.yaml
___
### Credenciais
Para que o processo ocorra de maneira segura e você possa acessar os repositórios, é necessário criar algumas secrets no kubernetes.
Para isso navegue até a pasta credentials:

    cd ./credentials

Abra arquivo "docker-credentials" com o editor de textos de sua preferência e onde esta o valor "<config.json base64>" coloque o valor das suas credenciais docker codificado em base64. Caso não saiba execute no terminal:

    cat ~/.docker/config.json | base64 -w 0

Caso não possua essas credenciais, consulte documentação [Docker](https://docs.docker.com/engine/reference/commandline/login/).

