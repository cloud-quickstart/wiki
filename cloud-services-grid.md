# Cloud Services Grid
in construction 2021-11

Use the new "All Products" page https://console.cloud.google.com/products

  `Service` | `category` | `GCP` | `GCP former` | `AWS` | `Azure` | `Open Source` | `Code Example` 
  --- | --- | --- | --- | --- | --- | --- | ---
  | | | | | | |
 CI/CD | | [Spinnaker](https://github.com/GoogleCloudPlatform/spinnaker-for-gcp) | | | | |
  | | | [Dataflow](https://cloud.google.com/dataflow) | | | | [Apache Beam](https://beam.apache.org/) |
 ML | | [Dataprep](https://cloud.google.com/dataflow) | | | | [Trifacta wranger](https://www.trifacta.com/) |
 Hadoop | | [Dataproc](https://cloud.google.com/dataproc) | | | | |
 DevOps | DevOps |  [DevOps](https://cloud.google.com/devops) [DORA - DevOps Research And Assessment](https://www.devops-research.com/quickcheck.html)] | | | | |
 Distributed Relational DBaaS | | [Bigtable](https://cloud.google.com/bigtable) | | | | Apache hbase |
 Event Handling | | [EventArc](https://cloud.google.com/eventarc/docs) | | EventBridge | | ||
 FaaS | Java Functions | [Functions Java](https://cloud.google.com/functions/docs/quickstart-java) | | | | |
 Java SDK | Java | [Java Client Libraries](https://github.com/googleapis/google-cloud-java) | | | | |
 Kubernetes | Security | [Gatekeeper](https://github.com/GoogleCloudPlatform/gatekeeper-securitycenter) : [GCP use of Gatekeeper](https://cloud.google.com/kubernetes-engine/docs/how-to/pod-security-policies-with-gatekeeper) | | [Open Policy Framework](https://github.com/open-policy-agent/gatekeeper) | |
 Kubernetes | Security | [Image trust using Notary](https://www.cncf.io/blog/2021/07/28/enforcing-image-trust-on-docker-containers-using-notary/) | | | |
 Kubernetes | serverless | Cloud Run | | Fargate | | knative with [CloudEvents](https://cloudevents.io/) capability | 
 MapReduce | | [Dataproc](https://cloud.google.com/dataproc) | | | | Apache Spark/Hadoop |
 Migrate | DB | | | | | |
 Migrate | VM | StratoZone and Migrate for CE | Velostrata | | | |
 Network | Tiered Network | [Premium Network tiers](https://cloud.google.com/network-tiers) | | | |
 Organizations (multiple) | IAM | [multiple orgs](https://cloud.google.com/resource-manager/docs/managing-multiple-orgs) | | | | |
 Private access | | [Private Service Connect](https://cloud.google.com/vpc/docs/private-service-connect)| | [VPC Endpoints](https://docs.aws.amazon.com/vpc/latest/privatelink/vpc-endpoints.html) | | |
 VPC | | | | | | | 
 VPC | CIDR | Dynamic CIDR resizing | | | | |
 VPC | Subnet across Regions | | | | | |
 VPC | SSH/RDP access | [Identity Aware Proxy](https://cloud.google.com/iap/docs/concepts-overview) | | | | |

## To categorize

Shared reservations across projects - https://cloud.google.com/compute/docs/instances/reservations-shared#best_practices

cloud composer off apache airflow
# Cross Cloud
## Categories
GCP on AWS
AWS on GCP
OSS on GCP

Karpenter

## To diagram
### Services in/output against other services - grid
### Heatmap



# Services
## Google Cloud Deploy
review: https://cloud.google.com/architecture/app-development-and-delivery-with-cloud-code-gcb-cd-and-gke?hl=en
https://cloud.google.com/deploy/docs/deploy-app-gke | https://cloud.google.com/blog/products/devops-sre/google-cloud-deploy-now-ga | 
https://cloud.google.com/deploy/docs/deploying-application/

## Google Policy Controller
https://cloud.google.com/blog/topics/anthos/enforcing-the-cis-benchmark-with-policy-controller | 

## Deployment Manager
Google Cloud Deployment Manager exports to Kubernetes Resource Model or Terraform - https://cloud.google.com/deployment-manager/docs/dm-convert?_ga=2.245568516.-1453179973.1650887889

## Kubernetes
https://www.protocol.com/enterprise/google-cloud-istio-cncf

