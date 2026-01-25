# PREREQUISITE
Download minikube

Install kubectl

Download Docker desktop

Enable virtualisation if you are using local computer to directly run minikube

## Install helm using choco
choco install kubernetes-helm

# DEPLOYING RESOURCE
## Deploying kubernetes
minikube start

## Enable ingress
minikube addons enable ingress

## Build docker image locally
eval $(minikube docker-env)
docker build -t fastapi-demo:1.0 . 

## Deploy db using helm
helm install db helm/postgres/

## Deploy webapp using helm
helm install webapp helm/appcharts/

## Deploy grafana
kubectl apply -f grafana-configmap.yaml

kubectl apply -f servicemonitor.yaml

helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

helm repo add grafana https://grafana.github.io/helm-charts

helm install kube-prom prometheus-community/kube-prometheus-stack \
  -n monitoring \
  --create-namespace \
  -f grafana-values.yaml


# Test app
Update local hostfile under C:\Windows\System32\drivers\etc\hosts add in a record for "127.0.0.1 api.local"

Open a browser and go to this link to monitor webhook updates https://webhook.site/#!/view/30cc039a-3e58-4e74-83f9-4860406ff233/a71f7c13-2ea3-4f2e-97cc-57832be70f05/1

Open another terminal and run command minikube tunnel

## API calls
curl -X POST "http://api.local/items?name=test"

curl -X GET "http://api.local/items"

curl -X PUT "http://api.local/items/1?name=updated"

curl -X DELETE "http://api.local/items/1"


you should be able to see the records as you enter these curl commands

Go back to the webhook page on your browser and you should see the POST requests



# Test grafana dashboard
## Get grafana password for log in page
kubectl --namespace monitoring get secrets kube-prom-grafana -o jsonpath="{.data.admin-password}" | base64 -d ; echo 

## set up port forwarding to grafana dashboard
kubectl port-forward -n monitoring svc/kube-prom-grafana 3000:80

## Open browser enter URL
http://localhost:3000

log in to console
username: admin
password: <from above step>

# Test prometheus alerts
## set up port forwarding to prometheus
kubectl port-forward -n monitoring svc/kube-prom-kube-prometheus-prometheus 9090:9090

## Open browser enter URL
http://localhost:9090

Go to Alerts tab, scroll to fastapi.rules and there you can see the prometheus rules threshold set