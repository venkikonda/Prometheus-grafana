# Prometheus-grafana

Fully fucntional monitoring solution for Kubernetes cluster.

<img src="https://raw.githubusercontent.com/srinisbook/images/master/Prometheus-grafana.png"
     alt="Prometheus and Grafana Architecture"
     style="float: left; margin-right: 10px;" />

Installation

Step 1: Clone repository

git clone https://github.com/srinisbook/Prometheus-grafana.git
cd Prometheus-grafana

Step 2: Apply the manifests

kubectl apply -f manifest/

Step 3: Create ingress for Garafana. If you don't have ingress controller, create loadbalancer service.
Update domain and ingress class in the grafana-ingress.yaml file and apply it.

kubectl apply -f grafana-ingress.yaml

Default credentilas are:

UserName: admin
Password: admin

Change Grafana credentials
Encode username and password in base64 format and update them in the manifests/05grafana-credentials-secret.yaml file

$ echo "admin" | base64
YWRtaW4K

$ echo "MyStrongPassword" | base64
TXlTdHJvbmdQYXNzd29yZAo=

data:
  admin-user: YWRtaW4=
  admin-password: TXlTdHJvbmdQYXNzd29yZAo=
  
kubectl apply -f manifests/05grafana-credentials-secret.yaml

Note: Make sure the delete the existing pod, new pod will create with updated credentials.

Get Grafana credentials:

echo "Username: $(kubectl get secret grafana --namespace prometheus \
                 --output=jsonpath='{.data.admin-user}' | base64 --decode)"
echo "Password: $(kubectl get secret grafana --namespace prometheus \
                 --output=jsonpath='{.data.admin-password}' | base64 --decode)"
