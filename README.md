# local-cluster
Local Kubernetes cluster configuration for bootit. Consists of:
- [flux](https://github.com/weaveworks/flux) for [GitOps](https://www.weave.works/blog/gitops-operations-by-pull-request)
- ELK stack for logging with filebeats
- bootit app

# Setup
This assumes you already have a functioning Kubernetes setup.
## Clone the repo
Do it.
## Private container registry access
The app should be available in a private docker registry. The current code assumes it is in ```ollireg.azurecr.io```. Kubernetes needs the credentials to access it so flux can perform CD.
```
kubectl create secret docker-registry regcred --docker-server=ollire
g.azurecr.io --docker-username=<registry user name> --docker-email=<email> --docker-password=<registry password>
```
## Let flux do its magic
Simply start flux to create the cluster
```
$ kubectl apply -f flux
```

# Kibana
To access the Kibana dashboard, go to ```http://localhost:5601/```


# Notes
## Kubernetes dashboard (insecure)
```
$ kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/master/src/deploy/alternative/kubernetes-dashboard.yaml
```
## Kubernetes graphs
```
$ kubectl create -f https://raw.githubusercontent.com/kubernetes/heapster/master/deploy/kube-config/influxdb/influxdb.yaml
$ kubectl create -f https://raw.githubusercontent.com/kubernetes/heapster/master/deploy/kube-config/influxdb/heapster.yaml
$ kubectl create -f https://raw.githubusercontent.com/kubernetes/heapster/master/deploy/kube-config/influxdb/grafana.yaml
```