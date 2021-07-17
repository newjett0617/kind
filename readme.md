# kind environment

## create cluster
```shell
kind create cluster --name kind --config ./kind.yaml
```

## deploy ingress controller
```shell
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml
```

### check ingress controller is ready
```shell
kubectl wait --namespace ingress-nginx \
  --for=condition=ready pod \
  --selector=app.kubernetes.io/component=controller \
  --timeout=90s
```

## creates simple services and ingress object
```shell
kubectl apply -f https://kind.sigs.k8s.io/examples/ingress/usage.yaml
```

### test
```shell
curl http://localhost/foo
# should output "foo"

curl http://localhost/bar
# should output "bar"
```

## delete services and ingress object
```shell
kubectl delete -f https://kind.sigs.k8s.io/examples/ingress/usage.yaml
```

## delete cluster
```shell
kind delete cluster --name kind
```