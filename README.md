# Kubernetes Primer

## Preparation

-) Install `yc` CLI (https://cloud.yandex.ru/docs/cli/quickstart#install)

```
curl -sSL https://storage.yandexcloud.net/yandexcloud-yc/install.sh | bash
```

-) Install `kubectl` (https://kubernetes.io/docs/tasks/tools/#kubectl)

```
brew install kubectl
```

-) Authenticate using a Google account

```
yc init --federation-id bpfnlok2em7ee652mj1e
```

-) Install `kubectx` (https://github.com/ahmetb/kubectx)

```
brew install kubectx
```

-) Add cluster credentials to kubeconfig

```
yc managed-kubernetes cluster get-credentials practicum-k8s --external
```

-) Test the access

```
kubectl get nodes
```

-) Install Helm (https://helm.sh/docs/intro/install/)

```
brew install helm
```

-) Install Lens (https://k8slens.dev/desktop.html)

## Create a sandbox

```
kubectl create ns <my_namespace>

kubens <my_namespace>
```

## Deploying the application. Imperative approach.

```
kubectl create deployment myapp --image=cr.yandex/crpab8haeuaugm6uqa9a/myapp:1.0.0

kubectl expose deployment/myapp --port=80 --target-port=3000
```

## Viewing resources

```
kubectl get pods

kubectl get deploy,rs,po -l app=myapp

kubectl get pod <pod-name> -o yaml

kubectl describe pods <pod-name>

kubectl get events
```

## Checking how selectors work

```
kubectl get pods --show-labels

kubectl label po <pod-name> app-

kubectl get pods --show-labels

kubectl label po <pod-name> app=myapp

kubectl get pods --show-labels
```

## Interacting with pods

```
kubectl logs <pod-name>

kubectl logs <pod-name> --previous

kubectl logs -f <pod-name> -c my-container

kubectl exec -it <pod-name> -- bash

kubectl port-forward <pod-name> 8080:3000

kubectl port-forward svc/myapp 8080:80
```

## Modifying resources

```
kubectl scale deployments/myapp --replicas=4

kubectl set image deployments/myapp myapp=cr.yandex/crpab8haeuaugm6uqa9a/myapp:2.0.0

kubectl rollout status deployments/myapp

kubectl rollout undo deployments/myapp

kubectl autoscale deployment myapp --cpu-percent=50 --min=2 --max=10
```

## Cleaning up

```
kubectl delete po <pod-name>

kubectl delete deployments/myapp services/myapp
```

## Managing the application. Declarative approach

```
kubectl create deployment myapp --image=myapp:v1 --dry-run=client -o yaml > deployment.yaml

kubectl expose deployment/myapp --port=80 --target-port=3000 --dry-run=client -o yaml > service.yaml

kubectl apply -f ./
```

## Helm

```
helm repo add bitnami https://charts.bitnami.com/bitnami

helm dependency update

helm template ./charts/myapp

helm upgrade -i myapp ./charts/myapp

helm upgrade -i --set redis.enabled=true --set envVars.redisHost=myapp-redis-master myapp ./charts/myapp
```