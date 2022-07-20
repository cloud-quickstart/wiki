# Google Cloud Deploy

# Links
- https://cloud.google.com/deploy
- https://kpt.dev/
- https://cloud.google.com/anthos-config-management/docs/concepts/config-controller-overview
- https://cloud.google.com/config-connector/docs/overview
- https://github.com/GoogleCloudPlatform/k8s-config-connector
- https://skaffold.dev/
- https://cloud.google.com/skaffold
- https://github.com/GoogleContainerTools/skaffold
- https://github.com/GoogleContainerTools/kpt-functions-catalog

## Quickstart

enable the anthos service first - or you will get unregistered anthos clusters (plain GKE clusters)

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



run 2
https://cloud.google.com/deploy/docs/deploy-app-gke?hl=en_US&_ga=2.18067903.769556588.1652289145-414126292.1645547024

<img width="953" alt="Screen Shot 2022-05-12 at 9 10 40 AM" src="https://user-images.githubusercontent.com/94715080/168082447-df42bc6f-3b6c-4eb2-9fc2-c1de8f8902df.png">

michael@cloudshell:~ (pubsec-declarative-toolkit-ns)$ gcloud projects add-iam-policy-binding $PROJECT_ID --member=serviceAccount:$(gcloud projects describe $PROJECT_ID --format="value(projectNumber)")-compute@developer.gserviceaccount.com  --role="roles/clouddeploy.jobRunner"
Updated IAM policy for project [pubsec-declarative-toolkit-ns].
bindings:
- members:
  - serviceAccoun
  
michael@cloudshell:~ (pubsec-declarative-toolkit-ns)$ gcloud projects add-iam-policy-binding $PROJECT_ID \
    --member=serviceAccount:$(gcloud projects describe $PROJECT_ID \
    --format="value(projectNumber)")-compute@developer.gserviceaccount.com \
    --role="roles/container.developer"
Updated IAM policy for project [pubsec-declarative-toolkit-ns].  
  

michael@cloudshell:~ (pubsec-declarative-toolkit-ns)$ gcloud container clusters create-auto quickstart-cluster-qsdev --project=$PROJECT_ID --region=us-central1 && gcloud container clusters create-auto quickstart-cluster-qsprod --project=$PROJECT_ID --region=us-central1
Note: The Pod address range limits the maximum size of the cluster. Please refer to https://cloud.google.com/kubernetes-engine/docs/how-to/flexible-pod-cidr to learn how to optimize IP address allocation.
Creating cluster quickstart-cluster-qsdev in us-central1... Cluster is being health-checked (master is healthy)...done.     
Created [https://container.googleapis.com/v1/projects/pubsec-declarative-toolkit-ns/zones/us-central1/clusters/quickstart-cluster-qsdev].
To inspect the contents of your cluster, go to: https://console.cloud.google.com/kubernetes/workload_/gcloud/us-central1/quickstart-cluster-qsdev?project=pubsec-declarative-toolkit-ns
kubeconfig entry generated for quickstart-cluster-qsdev.
NAME: quickstart-cluster-qsdev
LOCATION: us-central1
MASTER_VERSION: 1.21.10-gke.2000
MASTER_IP: 34.135.242.250
MACHINE_TYPE: e2-medium
NODE_VERSION: 1.21.10-gke.2000
NUM_NODES: 3
STATUS: RUNNING
Note: The Pod address range limits the maximum size of the cluster. Please refer to https://cloud.google.com/kubernetes-engine/docs/how-to/flexible-pod-cidr to learn how to optimize IP address allocation.
Creating cluster quickstart-cluster-qsprod in us-central1... Cluster is being deployed...working.    
Creating cluster quickstart-cluster-qsprod in us-central1... Cluster is being health-checked (master is healthy)...done.     
Created [https://container.googleapis.com/v1/projects/pubsec-declarative-toolkit-ns/zones/us-central1/clusters/quickstart-cluster-qsprod].
To inspect the contents of your cluster, go to: https://console.cloud.google.com/kubernetes/workload_/gcloud/us-central1/quickstart-cluster-qsprod?project=pubsec-declarative-toolkit-ns
kubeconfig entry generated for quickstart-cluster-qsprod.
NAME: quickstart-cluster-qsprod
LOCATION: us-central1
MASTER_VERSION: 1.21.10-gke.2000
MASTER_IP: 35.192.202.68
MACHINE_TYPE: e2-medium
NODE_VERSION: 1.21.10-gke.2000
NUM_NODES: 3
STATUS: RUNNING

michael@cloudshell:~ (pubsec-declarative-toolkit-ns)$ mkdir deploy-quickstart
michael@cloudshell:~ (pubsec-declarative-toolkit-ns)$ cd deploy-quickstart/
michael@cloudshell:~/deploy-quickstart (pubsec-declarative-toolkit-ns)$

michael@cloudshell:~/deploy-quickstart (pubsec-declarative-toolkit-ns)$ vi skaffold.yaml
apiVersion: skaffold/v2beta16
kind: Config
deploy:
  kubectl:
    manifests:
      - k8s-*
      

michael@cloudshell:~/deploy-quickstart (pubsec-declarative-toolkit-ns)$ vi k8s-pod.yaml
apiVersion: v1
kind: Pod
metadata:
  name: getting-started
spec:
  containers:
  - name: echoserver
    image: my-app-image
    
    
michael@cloudshell:~/deploy-quickstart (pubsec-declarative-toolkit-ns)$ vi clouddeploy.yaml
apiVersion: deploy.cloud.google.com/v1
kind: DeliveryPipeline
metadata:
 name: my-demo-app-1
description: main application pipeline
serialPipeline:
 stages:
 - targetId: qsdev
   profiles: []
 - targetId: qsprod
   profiles: []
---

apiVersion: deploy.cloud.google.com/v1
kind: Target
metadata:
 name: qsdev
description: development cluster
gke:
 cluster: projects/PROJECT_ID/locations/us-central1/clusters/quickstart-cluster-qsdev
---

apiVersion: deploy.cloud.google.com/v1
kind: Target
metadata:
 name: qsprod
description: production cluster
gke:
 cluster: projects/PROJECT_ID/locations/us-central1/clusters/quickstart-cluster-qsprod
 
replace your PROJECT_ID above

michael@cloudshell:~/deploy-quickstart (pubsec-declarative-toolkit-ns)$ gcloud deploy apply --file clouddeploy.yaml --region=us-central1 --project=pubsec-declarative-toolkit
API [clouddeploy.googleapis.com] not enabled on project [871599849367]. Would you like to enable and retry (this will take a few minutes)? (y/N)?  y

Enabling service [clouddeploy.googleapis.com] on project [871599849367]...
ERROR: (gcloud.deploy.apply) PERMISSION_DENIED: Permission denied to enable service [clouddeploy.googleapis.com]
Help Token: Ae-hA1P-Ogopd5_S0miqLnZiOcnG5YF_L3bP6C3NlGfw30lc4fgeAKnPKox5bpQLZBEv8dWCUIb9SSoKWWxdr_XUntrJsFbmNUylfWEvZ51vmPQI
- '@type': type.googleapis.com/google.rpc.PreconditionFailure
  violations:
  - subject: '110002'
    type: googleapis.com
- '@type': type.googleapis.com/google.rpc.ErrorInfo
  domain: serviceusage.googleapis.com
  reason: AUTH_PERMISSION_DENIED


```
remember to enable the APIs in the right project

<img width="597" alt="Screen Shot 2022-05-12 at 10 09 24 AM" src="https://user-images.githubusercontent.com/94715080/168094725-ce075b5e-ee27-4df7-b0e9-4803197e3bee.png">

```
still getting - check enabled services
michael@cloudshell:~/deploy-quickstart (pubsec-declarative-toolkit-ns)$ gcloud deploy apply --file clouddeploy.yaml --region=us-central1 --project=pubsec-declarative-toolkit
API [clouddeploy.googleapis.com] not enabled on project [871599849367]. Would you like to enable and retry (this will take a few minutes)? (y/N)?  y

Enabling service [clouddeploy.googleapis.com] on project [871599849367]...
ERROR: (gcloud.deploy.apply) PERMISSION_DENIED: Permission denied to enable service [clouddeploy.googleapis.com]
Help Token: Ae-hA1P-Ogopd5_S0miqLnZiOcnG5YF_L3bP6C3NlGfw30lc4fgeAKnPKox5bpQLZBEv8dWCUIb9SSoKWWxdr_XUntrJsFbmNUylfWEvZ51vmPQI
- '@type': type.googleapis.com/google.rpc.PreconditionFailure
  violations:
  - subject: '110002'
    type: googleapis.com
- '@type': type.googleapis.com/google.rpc.ErrorInfo
  domain: serviceusage.googleapis.com
  reason: AUTH_PERMISSION_DENIED
michael@cloudshell:~/deploy-quickstart (pubsec-declarative-toolkit-ns)$ gcloud deploy apply --file clouddeploy.yaml --region=us-central1 --project=pubsec-declarative-toolkit
API [clouddeploy.googleapis.com] not enabled on project [871599849367]. Would you like to enable and retry (this will take a few minutes)? (y/N)?  y

Enabling service [clouddeploy.googleapis.com] on project [871599849367]...
ERROR: (gcloud.deploy.apply) PERMISSION_DENIED: Permission denied to enable service [clouddeploy.googleapis.com]
Help Token: Ae-hA1MC0Y5wTwMuDD43Ih6YQ_m586u671QTD9T1fFATVc8LePkurheP5DySxxjxxY8l1d7d9ImqSj2XovulpJtN7EleY8ZHawzBs80GDePiJfpx
- '@type': type.googleapis.com/google.rpc.PreconditionFailure
  violations:
  - subject: '110002'
    type: googleapis.com
- '@type': type.googleapis.com/google.rpc.ErrorInfo
  domain: serviceusage.googleapis.com
  reason: AUTH_PERMISSION_DENIED
michael@cloudshell:~/deploy-quickstart (pubsec-declarative-toolkit-ns)$ gcloud services list --enabled --project pubsec-declarative-toolkit-ns
NAME: anthosconfigmanagement.googleapis.com
TITLE: Anthos Config Management API

NAME: autoscaling.googleapis.com
TITLE: Cloud Autoscaling API

NAME: bigquery.googleapis.com
TITLE: BigQuery API

NAME: bigquerymigration.googleapis.com
TITLE: BigQuery Migration API

NAME: bigquerystorage.googleapis.com
TITLE: BigQuery Storage API

NAME: cloudapis.googleapis.com
TITLE: Google Cloud APIs

NAME: cloudbuild.googleapis.com
TITLE: Cloud Build API

NAME: clouddebugger.googleapis.com
TITLE: Cloud Debugger API

NAME: clouddeploy.googleapis.com
TITLE: Google Cloud Deploy API

NAME: cloudresourcemanager.googleapis.com
TITLE: Cloud Resource Manager API

NAME: cloudtrace.googleapis.com
TITLE: Cloud Trace API

NAME: compute.googleapis.com
TITLE: Compute Engine API

NAME: container.googleapis.com
TITLE: Kubernetes Engine API

NAME: containerfilesystem.googleapis.com
TITLE: Container File System API

NAME: containerregistry.googleapis.com
TITLE: Container Registry API

NAME: datastore.googleapis.com
TITLE: Cloud Datastore API

NAME: gkeconnect.googleapis.com
TITLE: GKE Connect API

NAME: gkehub.googleapis.com
TITLE: GKE Hub API

NAME: iam.googleapis.com
TITLE: Identity and Access Management (IAM) API

NAME: iamcredentials.googleapis.com
TITLE: IAM Service Account Credentials API

NAME: krmapihosting.googleapis.com
TITLE: KRM API Hosting API

NAME: logging.googleapis.com
TITLE: Cloud Logging API

NAME: monitoring.googleapis.com
TITLE: Cloud Monitoring API

NAME: multiclustermetering.googleapis.com
TITLE: Multi cluster metering API

NAME: oslogin.googleapis.com
TITLE: Cloud OS Login API

NAME: pubsub.googleapis.com
TITLE: Cloud Pub/Sub API

NAME: servicemanagement.googleapis.com
TITLE: Service Management API

NAME: serviceusage.googleapis.com
TITLE: Service Usage API

NAME: sql-component.googleapis.com
TITLE: Cloud SQL

NAME: storage-api.googleapis.com
TITLE: Google Cloud Storage JSON API

NAME: storage-component.googleapis.com
TITLE: Cloud Storage

NAME: storage.googleapis.com
TITLE: Cloud Storage API


was about to post to cloud-deploy chat on service enabled not recognized - turned out I was missing a -ns postfix on my project name and was targeting "an existing" project in another account 871599849367  - I will stick to using $PROJECT_ID variables like your scripts - the less typing the better

PROJECT_ID: pubsec-declarative-toolkit-ns
NAME: pubsec-declarative-toolkit-ns
PROJECT_NUMBER: 1099466078563
michael@cloudshell:~/deploy-quickstart (pubsec-declarative-toolkit-ns)$ gcloud services list --enabled --project pubsec-declarative-toolkit-ns | grep deploy
NAME: clouddeploy.googleapis.com
michael@cloudshell:~/deploy-quickstart (pubsec-declarative-toolkit-ns)$ gcloud deploy apply --file clouddeploy.yaml --region=us-central1 --project=pubsec-declarative-toolkit
API [clouddeploy.googleapis.com] not enabled on project [871599849367]. Would you like to enable and retry (this will take a few minutes)? (y/N)?  ^C
Command killed by keyboard interrupt

michael@cloudshell:~/deploy-quickstart (pubsec-declarative-toolkit-ns)$ gcloud deploy apply --file clouddeploy.yaml --region=us-central1 --project=pubsec-declarative-toolkit-ns
Waiting for the operation on resource projects/pubsec-declarative-toolkit-ns/locations/us-central1/deliveryPipelines/my-demo-app-1...done.   
Created Cloud Deploy resource: projects/pubsec-declarative-toolkit-ns/locations/us-central1/deliveryPipelines/my-demo-app-1.
Waiting for the operation on resource projects/pubsec-declarative-toolkit-ns/locations/us-central1/targets/qsdev...done.   
Created Cloud Deploy resource: projects/pubsec-declarative-toolkit-ns/locations/us-central1/targets/qsdev.
Waiting for the operation on resource projects/pubsec-declarative-toolkit-ns/locations/us-central1/targets/qsprod...done.

```
<img width="1524" alt="Screen Shot 2022-05-12 at 10 33 32 AM" src="https://user-images.githubusercontent.com/94715080/168099902-65bfd370-cd46-4343-bb54-15437a4d298a.png">

<img width="1218" alt="Screen Shot 2022-05-12 at 10 34 04 AM" src="https://user-images.githubusercontent.com/94715080/168100012-66738fd3-d154-450c-b7e5-a7f79a919740.png">


```
run for GCP project
testing details

rerun on anthos $800k 30d trial nimbostratus.info

michael@cloudshell:~$ gcloud config set project pubsec-declarative-toolkit-ns
michael@cloudshell:~ (pubsec-declarative-toolkit-ns)$ unzip pubsec-declarative-toolkit.zip
set billing on the project (make sure or request for quota 20+ over the default 5)
michael@cloudshell:~ (pubsec-declarative-toolkit-ns)$ gcloud services enable krmapihosting.googleapis.com container.googleapis.com cloudresourcemanager.googleapis.com
Operation "operations/acf.p2-1099466078563-4545516c-39b2-4f2c-ad81-e97396659272" finished successfully.

e-hA1P6gyA86mXSWcVo3RqiY3Kfba8xzSymh3I01vIl05HG1_o8cMQJDn5eud8qO6ZxBo9_Bic7Z_JuFlCi2ZuXF50vmFmL1sYh9pRUoYyM9h_g
- '@type': type.googleapis.com/google.rpc.PreconditionFailure
  violations:
  - subject: ?error_code=390001&project=1099466078563&services=container.googleapis.com&services=container.googleapis.com&services=compute.googleapis.com&services=compute.googleapis.com&services=compute.googleapis.com&services=containerregistry.googleapis.com
    type: googleapis.com/billing-enabled
- '@type': type.googleapis.com/google.rpc.ErrorInfo
  domain: serviceusage.googleapis.com/billing-enabled
  metadata:
    project: '1099466078563'
    services: container.googleapis.com,container.googleapis.com,compute.googleapis.com,compute.googleapis.com,compute.googleapis.com,containerregistry.googleapis.com
  reason: UREQ_PROJECT_BILLING_NOT_FOUND
michael@cloudshell:~ (pubsec-declarative-toolkit-ns)$ gcloud services enable krmapihosting.googleapis.com container.googleapis.com cloudresourcemanager.googleapis.com
Operation "operations/acf.p2-1099466078563-4545516c-39b2-4f2c-ad81-e97396659272" finished successfully.
michael@cloudshell:~ (pubsec-declarative-toolkit-ns)$ PROJECT_ID=pubsec-declarative-toolkit-ns
michael@cloudshell:~ (pubsec-declarative-toolkit-ns)$ REGION=us-east1
michael@cloudshell:~ (pubsec-declarative-toolkit-ns)$ SUBNET=config-control
michael@cloudshell:~ (pubsec-declarative-toolkit-ns)$ NETWORK=config-control
michael@cloudshell:~ (pubsec-declarative-toolkit-ns)$ CLUSTER=config-controller
michael@cloudshell:~ (pubsec-declarative-toolkit-ns)$ gcloud compute networks create $NETWORK --subnet-mode=custom
Created [https://www.googleapis.com/compute/v1/projects/pubsec-declarative-toolkit-ns/global/networks/config-control].
NAME: config-control
SUBNET_MODE: CUSTOM
BGP_ROUTING_MODE: REGIONAL
IPV4_RANGE:
GATEWAY_IPV4:

Instances on this network will not be reachable until firewall rules
are created. As an example, you can allow all internal traffic between
instances as well as SSH, RDP, and ICMP by running:

$ gcloud compute firewall-rules create <FIREWALL_NAME> --network config-control --allow tcp,udp,icmp --source-ranges <IP_RANGE>
$ gcloud compute firewall-rules create <FIREWALL_NAME> --network config-control --allow tcp:22,tcp:3389,icmp


michael@cloudshell:~ (pubsec-declarative-toolkit-ns)$ gcloud compute networks subnets create $SUBNET --network $NETWORK --range 192.168.0.0/16 --region $REGION
Created [https://www.googleapis.com/compute/v1/projects/pubsec-declarative-toolkit-ns/regions/us-east1/subnetworks/config-control].
NAME: config-control
REGION: us-east1
NETWORK: config-control
RANGE: 192.168.0.0/16
STACK_TYPE: IPV4_ONLY
IPV6_ACCESS_TYPE:
INTERNAL_IPV6_PREFIX:
EXTERNAL_IPV6_PREFIX:

michael@cloudshell:~ (pubsec-declarative-toolkit-ns)$ gcloud anthos config controller create $CLUSTER --location $REGION --network $NETWORK --subnet $SUBNET
Create request issued for: [config-controller]
Waiting for operation [projects/pubsec-declarative-toolkit-ns/locations/us-east1/operations/operation-1652293623494-5dec0967e3790-ac228a1a-b61cfc97] to complete...working.

1428-1443 = 15min

michael@cloudshell:~ (pubsec-declarative-toolkit-ns)$ gcloud anthos config controller create $CLUSTER --location $REGION --network $NETWORK --subnet $SUBNET
Create request issued for: [config-controller]
Waiting for operation [projects/pubsec-declarative-toolkit-ns/locations/us-east1/operations/operation-1652293623494-5dec0967e3790-ac228a1a-b61cfc97] to complete...working.  
Waiting for operation [projects/pubsec-declarative-toolkit-ns/locations/us-east1/operations/operation-1652293623494-5dec0967e3790-ac228a1a-b61cfc97] to complete...working   
Waiting for operation [projects/pubsec-declarative-toolkit-ns/locations/us-east1/operations/operation-1652293623494-5dec0967e3790-ac228a1a-b61cfc97] to complete...working...
Waiting for operation [projects/pubsec-declarative-toolkit-ns/locations/us-east1/operations/operation-1652293623494-5dec0967e3790-ac228a1a-b61cfc97] to complete...working   
Waiting for operation [projects/pubsec-declarative-toolkit-ns/locations/us-east1/operations/operation-1652293623494-5dec0967e3790-ac228a1a-b61cfc97] to complete...done.     
Created instance [config-controller].
Fetching cluster endpoint and auth data.
kubeconfig entry generated for krmapihost-config-controller.
kubeconfig entry generated for krmapihost-config-controller.

efault Config Connector identity: [service-1099466078563@gcp-sa-yakima.iam.gserviceaccount.com].

For example, to give Config Connector permission to manage Google Cloud resources in the same project:
gcloud projects add-iam-policy-binding pubsec-declarative-toolkit-ns \
    --member "serviceAccount:service-1099466078563@gcp-sa-yakima.iam.gserviceaccount.com" \
    --role "roles/owner" \
    --project pubsec-declarative-toolkit-ns

from
gcloud container clusters get-credentials $CLUSTER --region $REGION
to
michael@cloudshell:~ (pubsec-declarative-toolkit-ns)$ gcloud container clusters get-credentials krmapihost-$CLUSTER --region $REGION
Fetching cluster endpoint and auth data.
kubeconfig entry generated for krmapihost-config-controller.

ael@cloudshell:~ (pubsec-declarative-toolkit-ns)$ kubens config-control
Context "gke_pubsec-declarative-toolkit-ns_us-east1_krmapihost-config-controller" modified.
Active namespace is "config-control".


michael@cloudshell:~ (pubsec-declarative-toolkit-ns)$ ORG_ID=$(gcloud projects get-ancestors $PROJECT_ID --format='get(id)' | tail -1)
michael@cloudshell:~ (pubsec-declarative-toolkit-ns)$ echo $ORG_ID
19...
michael@cloudshell:~ (pubsec-declarative-toolkit-ns)$ BILLING_ID=$(gcloud alpha billing projects describe $PROJECT_ID '--format=value(billingAccountName)' | sed 's/.*\///')
michael@cloudshell:~ (pubsec-declarative-toolkit-ns)$ echo $BILLING_ID
01...A5

michael@cloudshell:~ (pubsec-declarative-toolkit-ns)$ export ORG_ID=$ORG_ID
michael@cloudshell:~ (pubsec-declarative-toolkit-ns)$ export SA_EMAIL="$(kubectl get ConfigConnectorContext -n config-control \
    -o jsonpath='{.items[0].spec.googleServiceAccount}' 2> /dev/null)"
michael@cloudshell:~ (pubsec-declarative-toolkit-ns)$ echo $SA_EMAIL
service-10...63@gcp-sa-yakima.iam.gserviceaccount.com


michael@cloudshell:~ (pubsec-declarative-toolkit-ns)$ gcloud organizations add-iam-policy-binding "${ORG_ID}" --member "serviceAccount:${SA_EMAIL}" --role "roles/resourcemanager.folderAdmin"
Updated IAM policy for organization [197381943134].
auditConfigs:
- auditLogConfigs:
  - logType: DATA_WRITE
  - logType: DATA_READ
  - logType: ADMIN_READ
  service: allServices
bindings:
- members:
  - serviceAccount:tfadmin-dev@dev-seed-project.iam.gserviceaccount.com
  - serviceAccount:tfadmin2-dev@dev-seed-project.iam.gserviceaccount.com
  role: roles/accesscontextmanager.policyAdmin
- members:
  - serviceAccount:tfadmin-dev@dev-seed-project.iam.gserviceaccount.com
  - serviceAccount:tfadmin2-dev@dev-seed-project.iam.gserviceaccount.com
  role: roles/bigquery.dataEditor
- members:
  - group:gcp-billing-admins@nimbostratus.info
  - serviceAccount:tfadmin-dev@dev-seed-project.iam.gserviceaccount.com
  - user:superadmin@nimbostratus.info
  role: roles/billing.admin
- members:
  - domain:nimbostratus.info
  - group:gcp-billing-admins@nimbostratus.info
  role: roles/billing.creator
- members:
  - user:michael@nimbostratus.info
  role: roles/billing.projectManager
- members:
  - group:gcp-organization-admins@nimbostratus.info
  - serviceAccount:tfadmin-dev@dev-seed-project.iam.gserviceaccount.com
  - serviceAccount:tfadmin2-dev@dev-seed-project.iam.gserviceaccount.com
  role: roles/billing.user
- members:
  - group:billingdata@nimbostratus.info
  - group:sscbroker@nimbostratus.info
  role: roles/billing.viewer
- members:
  - group:sscbroker@nimbostratus.info
  role: roles/cloudasset.viewer
- members:
  - group:gcp-organization-admins@nimbostratus.info
  role: roles/cloudsupport.admin
- members:
  - serviceAccount:tfadmin-dev@dev-seed-project.iam.gserviceaccount.com
  role: roles/compute.admin
- members:
  - serviceAccount:tfadmin-dev@dev-seed-project.iam.gserviceaccount.com
  - serviceAccount:tfadmin2-dev@dev-seed-project.iam.gserviceaccount.com
  role: roles/compute.networkAdmin
- members:
  - serviceAccount:tfadmin-dev@dev-seed-project.iam.gserviceaccount.com
  - serviceAccount:tfadmin2-dev@dev-seed-project.iam.gserviceaccount.com
  role: roles/compute.xpnAdmin
- members:
  - group:gcp-organization-admins@nimbostratus.info
  - serviceAccount:tfadmin-dev@dev-seed-project.iam.gserviceaccount.com
  - serviceAccount:tfadmin2-dev@dev-seed-project.iam.gserviceaccount.com
  role: roles/iam.organizationRoleAdmin
- members:
  - serviceAccount:tfadmin-dev@dev-seed-project.iam.gserviceaccount.com
  role: roles/iam.securityAdmin
- members:
  - serviceAccount:tfadmin-dev@dev-seed-project.iam.gserviceaccount.com
  - serviceAccount:tfadmin2-dev@dev-seed-project.iam.gserviceaccount.com
  role: roles/iam.serviceAccountAdmin
- members:
  - serviceAccount:tfadmin-dev@dev-seed-project.iam.gserviceaccount.com
  - serviceAccount:tfadmin2-dev@dev-seed-project.iam.gserviceaccount.com
  - user:michael@nimbostratus.info
  role: roles/iam.serviceAccountTokenCreator
- members:
  - serviceAccount:tfadmin-dev@dev-seed-project.iam.gserviceaccount.com
  role: roles/logging.admin
- members:
  - serviceAccount:tfadmin-dev@dev-seed-project.iam.gserviceaccount.com
  - serviceAccount:tfadmin2-dev@dev-seed-project.iam.gserviceaccount.com
  role: roles/logging.configWriter
- members:
  - group:gcp-organization-admins@nimbostratus.info
  - serviceAccount:tfadmin-dev@dev-seed-project.iam.gserviceaccount.com
  - serviceAccount:tfadmin2-dev@dev-seed-project.iam.gserviceaccount.com
  - user:michael@nimbostratus.info
  role: roles/orgpolicy.policyAdmin
- members:
  - serviceAccount:tfadmin-dev@dev-seed-project.iam.gserviceaccount.com
  - user:michael@nimbostratus.info
  - user:superadmin@nimbostratus.info
  role: roles/owner
- members:
  - serviceAccount:tfadmin-dev@dev-seed-project.iam.gserviceaccount.com
  - serviceAccount:tfadmin2-dev@dev-seed-project.iam.gserviceaccount.com
  role: roles/pubsub.admin
- members:
  - group:gcp-organization-admins@nimbostratus.info
  - serviceAccount:service-1099466078563@gcp-sa-yakima.iam.gserviceaccount.com
  - serviceAccount:tfadmin-dev@dev-seed-project.iam.gserviceaccount.com
  - serviceAccount:tfadmin2-dev@dev-seed-project.iam.gserviceaccount.com
  - user:michael@nimbostratus.info
  - user:superadmin@nimbostratus.info
  role: roles/resourcemanager.folderAdmin
- members:
  - group:gcp-organization-admins@nimbostratus.info
  - serviceAccount:tfadmin-dev@dev-seed-project.iam.gserviceaccount.com
  - serviceAccount:tfadmin2-dev@dev-seed-project.iam.gserviceaccount.com
  - user:michael@nimbostratus.info
  - user:superadmin@nimbostratus.info
  role: roles/resourcemanager.organizationAdmin
- members:
  - group:gcp-billing-admins@nimbostratus.info
  role: roles/resourcemanager.organizationViewer
- members:
  - domain:nimbostratus.info
  - group:gcp-organization-admins@nimbostratus.info
  - serviceAccount:tfadmin-dev@dev-seed-project.iam.gserviceaccount.com
  - serviceAccount:tfadmin2-dev@dev-seed-project.iam.gserviceaccount.com
  - user:michael@nimbostratus.info
  role: roles/resourcemanager.projectCreator
- members:
  - serviceAccount:tfadmin-dev@dev-seed-project.iam.gserviceaccount.com
  - serviceAccount:tfadmin2-dev@dev-seed-project.iam.gserviceaccount.com
  role: roles/resourcemanager.projectDeleter
- members:
  - serviceAccount:tfadmin-dev@dev-seed-project.iam.gserviceaccount.com
  - serviceAccount:tfadmin2-dev@dev-seed-project.iam.gserviceaccount.com
  role: roles/resourcemanager.projectIamAdmin
- members:
  - serviceAccount:tfadmin-dev@dev-seed-project.iam.gserviceaccount.com
  - serviceAccount:tfadmin2-dev@dev-seed-project.iam.gserviceaccount.com
  role: roles/resourcemanager.projectMover
- members:
  - user:michael@nimbostratus.info
  role: roles/resourcemanager.tagAdmin
- members:
  - group:gcp-organization-admins@nimbostratus.info
  - user:michael@nimbostratus.info
  role: roles/securitycenter.admin
- members:
  - serviceAccount:tfadmin-dev@dev-seed-project.iam.gserviceaccount.com
  - serviceAccount:tfadmin2-dev@dev-seed-project.iam.gserviceaccount.com
  role: roles/serviceusage.serviceUsageAdmin
- members:
  - serviceAccount:tfadmin-dev@dev-seed-project.iam.gserviceaccount.com
  - serviceAccount:tfadmin2-dev@dev-seed-project.iam.gserviceaccount.com
  role: roles/storage.admin
etag: BwXewPlEjNA=
version: 1

michael@cloudshell:~ (pubsec-declarative-toolkit-ns)$ gcloud organizations add-iam-policy-binding "${ORG_ID}" --member "serviceAccount:${SA_EMAIL}" --role "roles/resourcemanager.folderAdmin"

michael@cloudshell:~ (pubsec-declarative-toolkit-ns)$ gcloud organizations add-iam-policy-binding "${ORG_ID}" --member "serviceAccount:${SA_EMAIL}" --role "roles/resourcemanager.projectCreator"

michael@cloudshell:~ (pubsec-declarative-toolkit-ns)$ gcloud organizations add-iam-policy-binding "${ORG_ID}" --member "serviceAccount:${SA_EMAIL}" --role "roles/resourcemanager.projectDeleter"

michael@cloudshell:~ (pubsec-declarative-toolkit-ns)$ gcloud organizations add-iam-policy-binding "${ORG_ID}" --member "serviceAccount:${SA_EMAIL}" --role "roles/orgpolicy.policyAdmin"

michael@cloudshell:~ (pubsec-declarative-toolkit-ns)$ gcloud organizations add-iam-policy-binding "${ORG_ID}" --member "serviceAccount:${SA_EMAIL}" --role "roles/iam.securityAdmin"

michael@cloudshell:~ (pubsec-declarative-toolkit-ns)$ gcloud organizations add-iam-policy-binding "${ORG_ID}" --member "serviceAccount:${SA_EMAIL}" --role "roles/serviceusage.serviceUsageConsumer"

michael@cloudshell:~ (pubsec-declarative-toolkit-ns)$ gcloud organizations add-iam-policy-binding "${ORG_ID}" --member "serviceAccount:${SA_EMAIL}" --role "roles/billing.user"


Thanks Chris - better creds

michael@cloudshell:~ (pubsec-declarative-toolkit-ns)$ gcloud anthos config controller get-credentials $CLUSTER --location $REGION
Fetching cluster endpoint and auth data.
kubeconfig entry generated for krmapihost-config-controller.
michael@cloudshell:~ (pubsec-declarative-toolkit-ns)$ kubens config-control
Context "gke_pubsec-declarative-toolkit-ns_us-east1_krmapihost-config-controller" modified.
Active namespace is "config-control".

```

## Deleting the Anthos cluster 
It will be unregistered in the anthos cluster console if anthos was not enabled previously - https://console.cloud.google.com/anthos/clusters?referrer=search&project=pubsec-declarative-toolkit-ns.  You may delete the underlying GKE cluster in https://console.cloud.google.com/kubernetes/list/overview?referrer=search&project=pubsec-declarative-toolkit-ns

https://cloud.google.com/anthos/docs/setup/disable-anthos
