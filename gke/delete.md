## delete
Delete GKE cluster
```
gcloud container clusters delete sample-cluster --zone "asia-southeast2-c" --project=${PROJECT}
```
Delete client VM
```
gcloud compute instances stop gke-client --zone asia-southeast2-c
```
Delete project
```
gcloud projects delete ${PROJECT}
```
