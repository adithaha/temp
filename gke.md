
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
PROJECT=gke-test-325311
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
```


# delete
```
gcloud container clusters delete sample-cluster --zone "asia-southeast2-c" --project=${PROJECT}
```
```
gcloud projects delete ${PROJECT}
```
