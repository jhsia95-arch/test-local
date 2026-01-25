# PREREQUISITE
Download minikube
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

## Deploy using helm
helm install webapp helm/appcharts/

update etc/host to 127.0.0.1 to service name api.local
minikube tunnel
choco install kubernetes-helm

   18  helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
   19  helm repo add grafana https://grafana.github.io/helm-charts
   20  helm install kube-prom prometheus-community/kube-prometheus-stack   -n monitoring --create-namespace

   23  minikube start --cpus=4 --memory=6g
   24  helm install kube-prom prometheus-community/kube-prometheus-stack   -n monitoring --create-namespace
   25  helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
   26  helm repo update
   27  helm install kube-prom prometheus-community/kube-prometheus-stack   -n monitoring   --create-namespace   --set grafana.enabled=true   --set alertmanager.enabled=true   --set prometheus.prometheusSpec.retention=2d
   28  kubectl get svc -n monitoring | grep prometheus
   29  kubectl apply -f k8s/postgres/
   30  kubectl apply -f k8s/app/
   31  curl -X POST "http://api.local/items?name=test"
   32  curl http://api.local/items
   33  history
   34  curl -X POST "http://192.168.49.2/items?name=test"
   35  kubectl get ingress
   36  curl -X POST "http://api.local/items?name=test"
   37  kubectl get nodes
   38  kubectl  get pods -A
   39  kubectl  get pods -Ao wide
   40  minikube ip
   41  curl -X POST "http://api.local/items?name=test"
   42  kubectl get svc -n ingress-nginx
   43  kubectl get pods -n ingress-nginx
minikube addons enable ingress
   48  minitunnel
   49  minikube tunnel
   50  kubectl get pods -n ingress-nginx
   51  curl -X POST "http://api.local/items?name=test"

   83  curl http://api.local/items
   84  curl -X POST "http://api.local/items?name=test"
   85  curl -X POST "http://api.local/items?name=test"
   86  curl http://api.local/items
curl -X POST "http://api.local/items?name=TestItem"
curl -X POST "http://api.local/items?name=TestItem"
curl -X GET "http://api.local/items"
curl -X DELETE "http://api.local/items/2"
curl -X PUT "http://api.local/items/2?name=UpdatedItem&price=30.0"


  119  curl -X POST "http://api.local/webhook" -H "Content-Type: application/json" -d '{"event":"manual_test"}'

kubectl port-forward -n monitoring svc/kube-prom-grafana 3000:80
  http://localhost:3000  
  kubectl --namespace monitoring get secrets kube-prom-grafana -o jsonpath="{.data.admin-password}" | base64 -d ; echo
   24  helm install kube-prom prometheus-community/kube-prometheus-stack   -n monitoring --create-namespace
   25  helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
   26  helm repo update
   27  helm install kube-prom prometheus-community/kube-prometheus-stack   -n monitoring   --create-namespace   --set grafana.enabled=true   --set alertmanager.enabled=true   --set prometheus.prometheusSpec.retention=2d

  125  helm upgrade --install kube-prom prometheus-community/kube-prometheus-stack   -n monitoring -f helm/grafana-values.yaml

  133  kubectl port-forward -n monitoring svc/kube-prom-kube-prometheus-prometheus 9090:9090
minikube stop
minikube start \
  --extra-config=kubelet.authentication-token-webhook=false \
  --extra-config=kubelet.authorization-mode=AlwaysAllow \
  --extra-config=kubelet.read-only-port=10255

to check if metrics eposed
kubectl port-forward -n default pod/fastapi-8594559996-m289r 8000:8000

100 - (avg by (instance) (rate(node_cpu_seconds_total{mode="idle"}[5m])) * 100)
100 * (1 - (node_memory_MemAvailable_bytes / node_memory_MemTotal_bytes))
100 * (1 - (node_filesystem_avail_bytes{fstype!~"tmpfs|rootfs"} / node_filesystem_size_bytes{fstype!~"tmpfs|rootfs"}))


