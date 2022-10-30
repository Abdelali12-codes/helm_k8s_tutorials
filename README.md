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
- or

```
helm search repo name-of-chart
```

- to create our own chart

```
helm create [Chart Name]
```

- to view the values of the chart

```
helm show values [Repo Name]/[Chart Name]
```

- store the default values of prometheus-mongodb-exporter and prometheus-mysql-exporter to set new values to combine them with the default one

```
helm show values prometheus-community/prometheus-mongodb-exporter > mongovalues.yaml
helm show values prometheus-community/prometheus-mysql-exporter > mysqlvalues.yaml
```

### 4. set the default namespace for your cluster

- the default namespace for the k8s cluster is default, to switch to another existed namespace

```
kubect config set-context --current --namespace monitoring
```

### 5. Configure Access to Multiple Clusters

- set user

```
kubectl config  set-credentials developer --client-certificate=fake-cert-file --client-key=fake-key-seefile
kubectl config  set-credentials developer --username=exp --password=some-password

```

- set cluster

```
kubectl config  set-cluster development --server=https://1.2.3.4 --certificate-authority=fake-ca-file

kubectl config  set-cluster scratch --server=https://5.6.7.8 --insecure-skip-tls-verify
```

- set context

```
kubectl config set-context dev-frontend --cluster=development --namespace=frontend --user=developer
```

- switch between contexts

```
kubectl config use-context [Name of Context]
```

- switch the namespace of the context

```
kubectl config set-context --current --namespace [Name of Namespace]
```

- view configuration associated with current-context

```
kubectl config view --minify
```

- delete user

```
kubectl config unset users.<name>

```

- delete cluster

```
kubectl config unset clusters.<name>
```

- delete context

```
kubectl config unset contexts.<name>
```

### 6. Configure Kubernetes Ingress using Helm

- install the repo on a specific namespace (ingress-nginx)

```
helm upgrade --install ingress-nginx ingress-nginx \
  --repo https://kubernetes.github.io/ingress-nginx \
  --namespace ingress-nginx --create-namespace
```

- or on the default using

```
helm upgrade --install ingress-nginx ingress-nginx \
  --repo https://kubernetes.github.io/ingress-nginx \
```

### 7. configuring the prometheus alert manager

- view the content of the altertmanager secret

```
kubectl get secret alertmanager-monitoring-kube-prometheus-alertmanager -n monitoring -o json
```

- delete the default secret of the prometheus alertmanager

```
kubectl delete secret alertmanager-monitoring-kube-prometheus-alertmanager -n monitoring
```

- create new secret with the same name from the alertmanager.yaml file (make sure to execute the below command on the directory where altermanager.yaml resides )

```
kubectl create secret generic alertmanager-monitoring-kube-prometheus-alertmanager --from-file=alertmanager.yaml
```

### 8. Helm commands

#### ways to install charts

- by reference a repo

```
helm repo add [Name of Repo] [Repo url]
```

- by pulling the chart to your local mahcine

```
helm pull [Chart Name]
```

- to untar your helm chart to a dir

```
helm pull [Char Name] --untar --untardir [directory]
```

#### chart Management

- create your own chart

```
helm create [Chart Name]
```

- show default values of a chart

```
helm show values [Chart Name]
```

- show chart definition

```
helm show chart [Chart Name]
```

- inspect a chart and its content

```
helm show all [Chart Name]
```
