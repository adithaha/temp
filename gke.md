
# admin

## create project

```
gcloud projects create --name=gke-test

PROJECT=[PROJECT_ID]
BILLING_ACCOUNT=[BILLING_ACCOUNT]

gcloud beta billing projects link ${PROJECT} --billing-account ${BILLING_ACCOUNT}
```

## create vpc
```
gcloud compute networks create devnet --project=gke-test-325306 --subnet-mode=custom --mtu=1460 --bgp-routing-mode=regional
gcloud compute networks subnets create jakarta --project=gke-test-325306 --range=10.148.0.0/20 --network=devnet --region=asia-southeast2
gcloud compute networks subnets create singapore --project=gke-test-325306 --range=10.146.0.0/20 --network=devnet --region=asia-southeast1
```

## enable policy with gui
```
gcloud resource-manager org-policies disable-enforce compute.vmCanIpForward --project=gke-test-325306
gcloud resource-manager org-policies disable-enforce compute.vmExternalIpAccess --project=gke-test-325306
```
```
gcloud resource-manager org-policies disable-enforce compute.requireShieldedVm --project=gke-test-325306
gcloud resource-manager org-policies disable-enforce compute.requireOsLogin --project=gke-test-325306
```
# dev
## create gke cluster
```
gcloud container clusters create sample-cluster --zone "asia-southeast2-c" --machine-type "e2-medium" --release-channel "stable" --network "devnet" --subnetwork "jakarta" --num-nodes 3 --enable-shielded-nodes
```


# delete
```
gcloud container clusters delete sample-cluster --zone "asia-southeast2-c"
```
```
gcloud projects delete ${PROJECT}
```
