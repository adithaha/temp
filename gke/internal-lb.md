# dev
```
PROJECT=[PROJECT_ID]
gcloud config set project ${PROJECT}

gcloud services enable compute.googleapis.com --project=${PROJECT}

gcloud compute instances create gke-client --machine-type e2-medium --zone asia-southeast2-c --network devnet --subnet jakarta
gcloud compute ssh --project=${PROJECT} --zone=asia-southeast2-c gke-client
```
