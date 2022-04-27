# Google Cloud Deploy

## Quickstart

https://cloud.google.com/deploy/docs/deploy-app-gke?_ga=2.236160513.-1647626204.1640188842

'''
michael@cloudshell:~ (clouddeploy-ol)$ gcloud container clusters create-auto quickstart-cluster-qsdev --project=clouddeploy-ol --region=us-central1 && gcloud container clusters create-auto quickstart-cluster-qsprod --project=clouddeploy-ol --region=us-central1
Note: The Pod address range limits the maximum size of the cluster. Please refer to https://cloud.google.com/kubernetes-engine/docs/how-to/flexible-pod-cidr to learn how to optimize IP address allocation.
Creating cluster quickstart-cluster-qsdev in us-central1... Cluster is being deployed...working   
'''
