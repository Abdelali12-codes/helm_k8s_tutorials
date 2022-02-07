# kubernetes_montoring_grafana_prometheus_third_party

We assume that you already seted up your k8s using minikube or other tools

# install prometheus and grafana using helm

- helm is a package manager for kubernetes as the apt for linux, pip for python.....

### 1. install helm

[!helm documentation](https://helm.sh/docs/intro/install/)

### 2. add the prometheus-operator

```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
```

### 3. install the chart

```
helm install [RELEASE_NAME] prometheus-community/kube-prometheus-stack
```

- if you want to install those charts on another namespace rather than default one

- first create a name space

```
kubectl create namespace monitoring
```

- then install the charts on the above namespace

```
helm install [RELEASE_NAME] prometheus-community/kube-prometheus-stack -n monitoring
```

- to list the projects on your repo

```
helm repo list
```

- to list charts installed on your cluster

```
helm list
```

- to remove the repo

```
helm repo remove [name of repo]
```

- to uninstall the charts from your cluster

```
helm uninstall [RELEASE NAME]
```

- to override the default values in the chart

```
helm install [RELEASE NAME]  -f myvalues.yaml [Chart Name]

```

- or

```
helm install [RELEASE NAME] --values myvalues.yaml [Chart Name]
```

- or

```

helm install [RELEASE NAME] --set key=value [Chart Name]

```

- to search for a repo

```
helm search repo [keywords of repo]
```

- to search for charts in repo

```
helm search hub [Name of repo] [keywords of chart]
```

- to create our own chart

```
helm create [Chart Name]
```

### 4. set the default namespace for your cluster

- the default namespace for the k8s cluster is default, to switch to another existed namespace

```
kubect config set-context --current --namespace monitoring
```
