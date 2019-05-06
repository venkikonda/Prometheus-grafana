# Kubernetes-Cluster-Monitoring

Kubernetes Cluster Monitoring with Prometheus and Grafana


***Set varibales***
```
export NAMESPACE="monitoring"
export GRAFANA_PASSWORD="$(pwgen 12 1 | tr -d '\n' | base64)"
export STORAGE_CLASS="" 
```
***Storage Class :***
  - Google Cloud : standard
  - AWS : gp2

***Substitute the variable values into the manifests and create a single yaml file***

```
awk 'FNR==1 {print "---"}{print}' manifest/* \ 
  | envsubst '$NAMESPACE $GRAFANA_PASSWORD $STORAGE_CLASS ' > "prometheus_grafana_manifest.yaml"
```
***Install Promenetheus-Grafana Stack***

````
kubectl apply -f prometheus_grafana_manifest.yaml
````

***Get Grafana credentials:***
```
echo "- user: $(kubectl get secret grafana --namespace $NAMESPACE \
                 --output=jsonpath='{.data.admin-user}' | base64 --decode)"
echo "- pass: $(kubectl get secret grafana --namespace $NAMESPACE \
                      --output=jsonpath='{.data.admin-password}' | base64 --decode)"
```
