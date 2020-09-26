# Kubernetes Ingress Example

## Setup the cluster:
```
kind create cluster --config=kind-ingress.yaml
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/static/provider/kind/deploy.yaml
```

## Wait for it to be ready:
```
kubectl wait --namespace ingress-nginx \
  --for=condition=ready pod \
  --selector=app.kubernetes.io/component=controller \
  --timeout=90s
```

Apply the apps and ingresss:
```
kubectl apply -f bar-app.yaml 
kubectl apply -f foo-app.yaml 
kubectl apply -f ingress.yaml  
```

## Test it out!

# should output "foo" and can be checked out in the browser too!
curl localhost/foo
# should output "bar"
curl localhost/bar


If you think you understand. run
`kind delete cluster`
then run the same steps but use the yaml file from the `challange` folder and see if you can't get it too work! :)
