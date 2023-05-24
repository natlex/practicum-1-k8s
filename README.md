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

-) `kubectl create ns <my_namespace>`

-) `kubens <my_namespace>`

## Deploy the application. Imperative approach
