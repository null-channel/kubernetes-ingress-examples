Setup the cluster:
kind create cluster --config=../kind-ingress.yaml
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/static/provider/kind/deploy.yaml

Wait for it to be read:
kubectl wait --namespace ingress-nginx \
  --for=condition=ready pod \
  --selector=app.kubernetes.io/component=controller \
  --timeout=90s

Apply the things:
kubectl apply -f bar-app.yaml
kubectl apply -f foo-app.yaml
kubectl apply -f ingress.yaml

## The challange, fix it!

 kind will be setup in a way to route localhost:80 too the ingress controller.

### should output "foo"
curl localhost/foo
### should output "bar"
curl localhost/bar

