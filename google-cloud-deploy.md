# Google Cloud Deploy

## Quickstart

https://cloud.google.com/deploy/docs/deploy-app-gke?_ga=2.236160513.-1647626204.1640188842

```
michael@cloudshell:~ (clouddeploy-ol)$ gcloud container clusters create-auto quickstart-cluster-qsdev --project=clouddeploy-ol --region=us-central1 && gcloud container clusters create-auto quickstart-cluster-qsprod --project=clouddeploy-ol --region=us-central1
Note: The Pod address range limits the maximum size of the cluster. Please refer to https://cloud.google.com/kubernetes-engine/docs/how-to/flexible-pod-cidr to learn how to optimize IP address allocation.
Creating cluster quickstart-cluster-qsdev in us-central1... Cluster is being deployed...working 

5min

Creating cluster quickstart-cluster-qsdev in us-central1... Cluster is being health-checked (master is healthy)...working. 
Created [https://container.googleapis.com/v1/projects/clouddeploy-ol/zones/us-central1/clusters/quickstart-cluster-qsdev].
To inspect the contents of your cluster, go to: https://console.cloud.google.com/kubernetes/workload_/gcloud/us-central1/quickstart-cluster-qsdev?project=clouddeploy-ol
kubeconfig entry generated for quickstart-cluster-qsdev.
NAME: quickstart-cluster-qsdev
LOCATION: us-central1
MASTER_VERSION: 1.21.6-gke.1503
MASTER_IP: 35.188.77.181
MACHINE_TYPE: e2-medium
NODE_VERSION: 1.21.6-gke.1503
NUM_NODES: 3
STATUS: RUNNING
Note: The Pod address range limits the maximum size of the cluster. Please refer to https://cloud.google.com/kubernetes-engine/docs/how-to/flexible-pod-cidr to learn how to optimize IP address allocation.
Creating cluster quickstart-cluster-qsprod in us-central1...working..
```


https://cloud.google.com/anthos/docs/setup/disable-anthos
