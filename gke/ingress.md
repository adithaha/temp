
# Setup access via Ingress

## Go to GKE cluster
```
gcloud container clusters get-credentials sample-cluster --zone ${REGION1}-c --project=${PROJECT}
kubectl config set-context --current --namespace=sample-app
```

## Deploy second app
```
kubectl apply -f ingress/deployment.yaml
```
## External Ingress
Create service nodeport
```
kubectl create -f ingress/service-nodeport.yaml
kubectl get svc
```
Create ingress
```
kubectl create -f ingress/ingress.yaml
```
## Access App using Ingress
Get LB address with command below, may need some time to get it
```
kubectl get ingress
```

