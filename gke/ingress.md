
# Setup access via Ingress

## Go to GCP project
```
PROJECT=[PROJECT_ID]
gcloud config set project ${PROJECT}
```
## Go to GKE cluster
```
gcloud container clusters get-credentials sample-cluster --zone "asia-southeast2-c" --project=${PROJECT}
kubectl config set-context --current --namespace=sample-app
```
## External Ingress
Create service nodeport
```
kubectl create -f service-nodeport.yaml
kubectl get svc
```
Create ingress
```
kubectl create -f ingress.yaml
kubectl get svc
```
