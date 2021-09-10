
# admin

## create project

```
gcloud projects create --name=gke-test

PROJECT=[PROJECT_ID]
BILLING_ACCOUNT=[BILLING_ACCOUNT]

gcloud beta billing projects link ${PROJECT} --billing-account ${BILLING_ACCOUNT}
```
```
gcloud projects add-iam-policy-binding ${PROJECT} --member=user:[USER_EMAIL] --role=roles/owner
```
## enable policy with gui
```
gcloud resource-manager org-policies disable-enforce compute.vmCanIpForward --project=${PROJECT}
gcloud resource-manager org-policies disable-enforce compute.vmExternalIpAccess --project=${PROJECT}
```
```
gcloud resource-manager org-policies disable-enforce compute.requireShieldedVm --project=${PROJECT}
gcloud resource-manager org-policies disable-enforce compute.requireOsLogin --project=${PROJECT}
```
# dev
```
PROJECT=[PROJECT_ID]
gcloud config set project ${PROJECT}
```
## create vpc
```
gcloud compute networks create devnet --project=${PROJECT} --subnet-mode=custom --mtu=1460 --bgp-routing-mode=regional
gcloud compute networks subnets create jakarta --project=${PROJECT} --range=10.148.0.0/20 --network=devnet --region=asia-southeast2
gcloud compute networks subnets create singapore --project=${PROJECT} --range=10.146.0.0/20 --network=devnet --region=asia-southeast1
```
## create gke cluster
```
gcloud services enable container.googleapis.com --project=${PROJECT}
gcloud container clusters create sample-cluster --zone "asia-southeast2-c" --machine-type "e2-medium" --release-channel "stable" --network "devnet" --subnetwork "jakarta" --num-nodes 3 --enable-shielded-nodes --project=${PROJECT}
gcloud container clusters get-credentials sample-cluster --zone "asia-southeast2-c" --project=${PROJECT}
```
## deploy Hello App

Create namespace
```
kubectl create namespace sample-app
kubectl config set-context --current --namespace=sample-app
kubectl config view --minify | grep namespace:
```
Deploy Hello App
```
kubectl apply -f deployment.yaml
kubectl describe deployment hello-app-deployment
kubectl get pods -l app=hello-app
POD_NAME=[POD_NAME]
```
Get logs and enter shell
```
kubectl logs -f ${POD_NAME}
kubectl exec -i -t ${POD_NAME} -- /bin/bash
```
## External Load balancer
Create external lb
```
kubectl create service loadbalancer hello-app --tcp=8080:8080
kubectl get svc
```