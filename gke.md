gcloud compute networks create devnet --project=gke-test-325306 --subnet-mode=custom --mtu=1460 --bgp-routing-mode=regional
gcloud compute networks subnets create jakarta --project=gke-test-325306 --range=10.148.0.0/20 --network=devnet --region=asia-southeast2
gcloud compute networks subnets create singapore --project=gke-test-325306 --range=10.146.0.0/20 --network=devnet --region=asia-southeast1


# create gke cluster
gcloud container clusters create sample-cluster --zone "asia-southeast2-c" --machine-type "e2-medium" --release-channel "stable" --network "devnet" --subnetwork "jakarta" --num-nodes 3

gcloud container clusters delete sample-cluster --zone "asia-southeast1-c" --network "devnet" --subnetwork "singapore"

