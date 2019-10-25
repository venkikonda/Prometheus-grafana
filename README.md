# Prometheus-grafana

Fully fucntional monitoring solution for Kubernetes cluster.

<img src="https://raw.githubusercontent.com/srinisbook/images/master/Prometheus-grafana.png"
     alt="Prometheus and Grafana Architecture"
     style="float: left; margin-right: 10px;" />

***Create a single manifest file***
```
awk 'FNR==1 {print "---"}{print}' manifests/* > "prometheus_grafana_manifest.yaml"
```
***Install Promenetheus-Grafana Stack***
````
kubectl apply -f prometheus_grafana_manifest.yaml
````

***Get Grafana credentials:***
```
echo "Username: $(kubectl get secret grafana --namespace prometheus \
                 --output=jsonpath='{.data.admin-user}' | base64 --decode)"
echo "Password: $(kubectl get secret grafana --namespace prometheus \
                 --output=jsonpath='{.data.admin-password}' | base64 --decode)"
```
