
# dev
```
PROJECT=[PROJECT_ID]
gcloud config set project ${PROJECT}
```
## External Ingress
Create nodeport
```
kubectl create -f service-nodeport.yaml
kubectl get svc
```

Create ingress
```
kubectl create -f ingress.yaml
kubectl get svc
```