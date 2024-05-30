# Treinamento GitOps

## Pré-requisitos

- Instalar o Minikube ou Kind
- Instalar o jq no terminal
- Helm para criar um chart

## Inicializar o Minikube

No terminal

```
minikube start
```

## Instalar o ArgoCD

```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

## Mapeamento para porta local

O encaminhamento de porta Kubectl também pode ser usado para conectar-se ao servidor API sem expor o serviço.

```
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

## Descobrir a senha inicial

```
kubectl get secrets argocd-initial-admin-secret -n argocd -o json | jq -r .data.password | base64 -d
```

## Acessar o ArgoCD

```
http://localhost:8080
```

## Criar o SSH Private Key para se conectar no repositório de infra

1. Crie um chave privada/publica
```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

2.  A publica configure no Azure Devops no caminho Clone Repository / SSH / Manage SSH Keys / ADD
3.  A privada utilize no ArgoCD em Settings / Repositories / Via SSH

## Crie a aplicação no ArgoCD

Acesse Application / Create Application

- Application name: app1
- Project name: default
- Source
  - Repository URL: (busque a configuração que fez anteriormente)
  - Path: selecione a pasta que está a aplicação no caso (app1)
- Destination
  - Cluster URL: https://kubernetes.default.svc
  - Namespace: default
    
Create!

Clique na opção "Sync"
