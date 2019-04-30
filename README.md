# Kubernetes-Cluster-Monitoring
Kubernetes Cluster Monitoring with Prometheus and Grafana

***Storage Class :***
  - Google Cloud : standard
  - AWS : gp2
```
export NAMESPACE="promgrafana"

export GRAFANA_PASSWORD="$(pwgen 12 1 | tr -d '\n' | base64)"

export STORAGE_CLASS="" 
```



awk 'FNR==1 {print "---"}{print}' manifest/* \ 
  | envsubst '$NAMESPACE $GRAFANA_PASSWORD $STORAGE_CLASS ' > "prometheus_grafana_manifest.yaml"
  
```
echo "Grafana credentials:"

echo "- user: $(kubectl get secret grafana --namespace $NAMESPACE \
                 --output=jsonpath='{.data.admin-user}' | base64 --decode)"
echo "- pass: $(kubectl get secret grafana --namespace $NAMESPACE \
                      --output=jsonpath='{.data.admin-password}' | base64 --decode)"
```
