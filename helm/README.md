# Helm

```sh
# Create k8s-cluster
kind create cluster \
  --image kindest/node:v1.33.1 \
  --config kind-cluster.yaml \
  --name kind-cluster

# List all kind clusters
kind get clusters

# Delete cluster
kind delete clusters kind-cluster

# K8S Nodes
kubectl get nodes -o wide

# Generating YAML manifests
helm template kube-prometheus-stack --debug --dry-run --namespace monitoring --create-namespace -f kube-prometheus-stack/custom-values.yaml . > kube-prometheus-stack.yaml

# Install helm from file
cd kube-prometheus-stack
helm install kube-prometheus-stack \
  --namespace monitoring \
  --create-namespace  \
  --values custom-values.yaml \
  .

# Get all resources
kubectl get all --namespace monitoring
```

```sh
#
cd charts/ingress-nginx
helm install ingress-nginx \
  --namespace ingress-nginx \
  --create-namespace \
  -f custom-values.yaml \
  .

```
