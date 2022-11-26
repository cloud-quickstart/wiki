# Kubernetes
## Kubernetes Engine: Qwik Start
- duration 21 min of 30
- Note this lab may time out on us-central-1 periodically - taking up to 35 min to provision a GKE standard cluster instead of the usual 5.  If you restart the lab and get another region like us-west - GKE will start in around 10 min OK

```
Welcome to Cloud Shell! Type "help" to get started.
Your Cloud Platform project in this session is set to qwiklabs-gcp-02-aba13b76dd6e.
Use “gcloud config set project [PROJECT_ID]” to change to a different project.
student_02_aa60c540468a@cloudshell:~ (qwiklabs-gcp-02-aba13b76dd6e)$ gcloud auth list
Credentialed Accounts

ACTIVE: *
ACCOUNT: student-02-aa60c540468a@qwiklabs.net

To set the active account, run:
    $ gcloud config set account `ACCOUNT`

student_02_aa60c540468a@cloudshell:~ (qwiklabs-gcp-02-aba13b76dd6e)$ gcloud config list project
[core]
project = qwiklabs-gcp-02-aba13b76dd6e

Your active configuration is: [cloudshell-7747]
student_02_aa60c540468a@cloudshell:~ (qwiklabs-gcp-02-aba13b76dd6e)$ gcloud config set compute/region us-west1
Updated property [compute/region].
student_02_aa60c540468a@cloudshell:~ (qwiklabs-gcp-02-aba13b76dd6e)$ gcloud config set compute/zone us-west1-c
Updated property [compute/zone].
student_02_aa60c540468a@cloudshell:~ (qwiklabs-gcp-02-aba13b76dd6e)$ gcloud container clusters create --machine-type=e2-medium --zone=us-west1-c lab-cluster 
Default change: VPC-native is the default mode during cluster creation for versions greater than 1.21.0-gke.1500. To create advanced routes based clusters, please pass the `--no-enable-ip-alias` flag
Default change: During creation of nodepools or autoscaling configuration changes for cluster versions greater than 1.24.1-gke.800 a default location policy is applied. For Spot and PVM it defaults to ANY, and forall other VM kinds a BALANCED policy is used. To change the default values use the `--location-policy` flag.
Note: Your Pod address range (`--cluster-ipv4-cidr`) can accommodate at most 1008 node(s).
Creating cluster lab-cluster in us-west1-c... Cluster is being health-checked (master is healthy)...workin
g...
Creating cluster lab-cluster in us-west1-c... Cluster is being health-checked (master is healthy)...done.
Created [https://container.googleapis.com/v1/projects/qwiklabs-gcp-02-aba13b76dd6e/zones/us-west1-c/clusters/lab-cluster].
To inspect the contents of your cluster, go to: https://console.cloud.google.com/kubernetes/workload_/gcloud/us-west1-c/lab-cluster?project=qwiklabs-gcp-02-aba13b76dd6e
kubeconfig entry generated for lab-cluster.
NAME: lab-cluster
LOCATION: us-west1-c
MASTER_VERSION: 1.23.12-gke.100
MASTER_IP: 35.227.174.84
MACHINE_TYPE: e2-medium
NODE_VERSION: 1.23.12-gke.100
NUM_NODES: 3
STATUS: RUNNING
student_02_aa60c540468a@cloudshell:~ (qwiklabs-gcp-02-aba13b76dd6e)$ gcloud container clusters get-credentials lab-cluster 
Fetching cluster endpoint and auth data.
kubeconfig entry generated for lab-cluster.
student_02_aa60c540468a@cloudshell:~ (qwiklabs-gcp-02-aba13b76dd6e)$ kubectl create deployment hello-server --image=gcr.io/google-samples/hello-app:1.0
deployment.apps/hello-server created
student_02_aa60c540468a@cloudshell:~ (qwiklabs-gcp-02-aba13b76dd6e)$ kubectl expose deployment hello-server --type=LoadBalancer --port 8080
service/hello-server exposed
student_02_aa60c540468a@cloudshell:~ (qwiklabs-gcp-02-aba13b76dd6e)$ kubectl get service
NAME           TYPE           CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
hello-server   LoadBalancer   10.64.14.207   <pending>     8080:30928/TCP   10s
kubernetes     ClusterIP      10.64.0.1      <none>        443/TCP          4m37s
student_02_aa60c540468a@cloudshell:~ (qwiklabs-gcp-02-aba13b76dd6e)$ kubectl get service
NAME           TYPE           CLUSTER-IP     EXTERNAL-IP     PORT(S)          AGE
hello-server   LoadBalancer   10.64.14.207   34.82.144.104   8080:30928/TCP   39s
kubernetes     ClusterIP      10.64.0.1      <none>          443/TCP          5m6s
student_02_aa60c540468a@cloudshell:~ (qwiklabs-gcp-02-aba13b76dd6e)$ wget http://34.82.144.104:8080
--2022-11-26 15:22:12--  http://34.82.144.104:8080/
Connecting to 34.82.144.104:8080... connected.
HTTP request sent, awaiting response... 200 OK
Length: 69 [text/plain]
Saving to: ‘index.html’

index.html                           100%[===================================================================>]      69  --.-KB/s    in 0s

2022-11-26 15:22:13 (10.6 MB/s) - ‘index.html’ saved [69/69]

student_02_aa60c540468a@cloudshell:~ (qwiklabs-gcp-02-aba13b76dd6e)$ gcloud container clusters delete lab-cluster 
The following clusters will be deleted.
 - [lab-cluster] in [us-west1-c]

Do you want to continue (Y/n)?  y

Deleting cluster lab-cluster...working 
Deleting cluster lab-cluster...done.     
Deleted [https://container.googleapis.com/v1/projects/qwiklabs-gcp-02-aba13b76dd6e/zones/us-west1-c/clusters/lab-cluster].
```
