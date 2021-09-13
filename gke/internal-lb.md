# Internal Load Balancer
Setup internal load balancer, and test from client VM



# Create Internal LB
```
kubectl config set-context --current --namespace=sample-app
kubectl apply -f ilb/service.yaml
```
Check load balancer IP
```
kubectl get svc
```

# Create Client VM
```
PROJECT=[PROJECT_ID]
gcloud config set project ${PROJECT}
gcloud services enable compute.googleapis.com --project=${PROJECT}
gcloud compute instances create gke-client --machine-type e2-medium --zone asia-southeast2-c --network devnet --subnet jakarta
```

# Call App from client VM
SSH into vlient VM
```
gcloud compute ssh --project=${PROJECT} --zone=asia-southeast2-c gke-client
```
Call Hello App using internal load balancer
```
curl <IP-INTERNAL-LB>:8080
```

### Go back
[Content](https://github.com/adithaha/temp/blob/main/gke/readme.md)
