# Treinamento GitOps

## Pré-requisitos

- Instalar o Minikube ou Kind
- Instalar o jq no terminal

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
