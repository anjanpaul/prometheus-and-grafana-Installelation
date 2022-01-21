# add prometheus Helm repo
```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

```

# add grafana Helm repo
```
helm repo add grafana https://grafana.github.io/helm-charts

```
# Create a new Namespace
```
kubectl create namespace prometheus

```
# Install prometheus with helm

```

helm install prometheus prometheus-community/prometheus \
    --namespace prometheus \
    --set alertmanager.persistentVolume.storageClass="gp2" \
    --set server.persistentVolume.storageClass="gp2"

```

## Make note of the prometheus endpoint in helm response (you will need this later). It should look similar to below: 
```
The Prometheus server can be accessed via port 80 on the following DNS name from within your cluster:
prometheus-server.prometheus.svc.cluster.local

```

# Check if Prometheus components deployed as expected
```
kubectl get all -n prometheus

```
# You should see response similar to below. They should all be Ready and Available

![alt text](https://github.com/anjanpaul/prometheus-and-grafana-Installelation/blob/main/Deployed%20Vesion.png)


# In order to access the Prometheus server URL, we are going to use the kubectl port-forward command to access the application.

```
kubectl port-forward -n prometheus deploy/prometheus-server 8080:9090

```