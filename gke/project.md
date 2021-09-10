
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
## create firewall
```
gcloud compute firewall-rules create allow-ssh-ingress-from-iap \
  --direction=INGRESS \
  --action=allow \
  --rules=tcp:22 \
  --source-ranges=35.235.240.0/20 \
  --project=${PROJECT} \
  --network=devnet
```