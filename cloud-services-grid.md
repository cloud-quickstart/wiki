# Cloud Services Grid
in construction 2021-11

- Use the new "All Products" page https://console.cloud.google.com/products
- https://cloud.google.com/free/docs/aws-azure-gcp-service-comparison

  `Service` | `category` | `GCP` | `GCP former` | `AWS` | `Azure` | `Open Source` | `Code Example` 
  --- | --- | --- | --- | --- | --- | --- | ---
  | | | | | | |
 CI/CD | | [Spinnaker](https://github.com/GoogleCloudPlatform/spinnaker-for-gcp) | | | | |
  | | | [Dataflow](https://cloud.google.com/dataflow) | | | | [Apache Beam](https://beam.apache.org/) |
 ML | | [Dataprep](https://cloud.google.com/dataflow) | | | | [Trifacta wranger](https://www.trifacta.com/) |
 Hadoop | | [Dataproc](https://cloud.google.com/dataproc) | | | | |
 Data Warehouse | | [BigQuery](https://github.com/cloud-quickstart/wiki/blob/main/google-training.md#bigquery) | | | |  |
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
 Spot VMs | | [Spot VMs](https://cloud.google.com/spot-vms) | | | | | 
 VPC | | | | | | | 
 VPC | CIDR | Dynamic CIDR resizing | | | | |
 VPC | Subnet across Regions | | | | | |
 VPC | SSH/RDP access | [Identity Aware Proxy](https://cloud.google.com/iap/docs/concepts-overview) | | | | |


  AI	Video AI	Amazon Rekognition Video
API management	Apigee API Management	Amazon API Gateway
Audit logging	Cloud Audit Logs	AWS CloudTrail
Block storage	Persistent Disk	Amazon Elastic Block Store (EBS)
Build	Cloud Storage for Firebase	AWS Simple Storage Service (S3)
Build	Firebase Auth	Amazon Cognito
Build	Firebase Hosting	AWS Simple Storage Service (S3)
Build	Firebase Realtime Database	AWS DynamoDB + AppSync
Business intelligence	Looker	Amazon QuickSight
CaaS	Google Kubernetes Engine	Amazon Elastic Kubernetes Service (EKS),
Amazon Elastic Container Service (ECS)
CDN	Cloud CDN	Amazon CloudFront
Certificate management	Certificate Authority Service	AWS Certificate Manager
CI/CD	Cloud Build	AWS CodeBuild,
AWS CodeDeploy,
AWS CodePipeline
CIAM	Identity Platform	Amazon Cognito
Client libraries	Cloud SDK	AWS SDKs
Cloud cost optimization	Recommender	AWS Cost Optimization
Cloud development IDE plugin	Cloud Code for IntelliJ	AWS Toolkit for IntelliJ
Cloud development IDE plugin	Cloud Code for VS Code	AWS Toolkit for Visual Studio Code
Cloud-based IDE	Cloud Shell	AWS CloudShell
Command-line interface (CLI)	Cloud SDK	AWS CLI
Container migration	Migrate for Anthos	AWS App2Container
Container registry	Artifact Registry	Amazon Elastic Container Registry (ECR)
Container Security	Binary Authorization	
Container security	Artifact Registry	Amazon Elastic Container Registry (ECR)
Container security	Container Analysis	Amazon ECR Image Scanning
Container security	Container Security	Security in Amazon Elastic Container Service (ECS)
Container security	GKE Sandbox	Amazon EKS Container Sandbox
Containers without infrastructure	Cloud Run	AWS Fargate, AWS Lambda, AWS App Runner
Conversational interface	Dialogflow	Amazon Lex
Core compute	Cloud GPUs	Amazon Elastic Compute Cloud (EC2) P3
Core compute	Compute Engine	Amazon Elastic Compute Cloud (EC2)
Core compute	Compute Engine Autoscaler	AWS Autoscaling
Core compute	OS Login	Amazon EC2 Instance Connect
Core compute	Persistent Disk	Amazon Elastic Block Store (EBS)
Core compute	SSH from the browser	AWS EC2 Instance Connect
Cost management	Cost Management	AWS Budgets
Data discovery and metadata management	Data Catalog	AWS Glue Data Catalog
Data Integration / ETL	Cloud Data Fusion	Amazon AppFlow, Amazon Data Pipeline, AWS Glue
Data loss prevention (DLP)	Cloud Data Loss Prevention	Amazon Macie
Data warehouse	BigQuery	Amazon Athena, Amazon Redshift
DDoS firewall	Google Cloud Armor Managed Protection	AWS Shield Basic/Advanced
Debugging	Cloud Debugger	AWS X-Ray
Dedicated Interconnect connection	Cloud Interconnect	AWS Direct Connect
Dedicated VMs	Sole-tenant nodes	Amazon EC2 Dedicated Host
Deployment	Cloud Deployment Manager	AWS CloudFormation
Document data storage	Firestore	Amazon DocumentDB, AWS DynamoDB,
AWS AppSync
Domains and DNS	Cloud DNS	Amazon Route 53
Domains and DNS	Cloud Domains	Amazon Route 53
Encoding	Transcoder API	AWS Media Converter
Encryption	Confidential Computing	AWS Nitro Enclaves
Engage	Firebase A/B Testing	Amazon Pinpoint
Engage	Firebase Cloud Messaging	Amazon Device Messaging (ADM),
Amazon Simple Notification Service (SNS)
Engage	Firebase Dynamic Links	
Engage	Firebase In-App Messaging	Amazon Device Messaging (ADM),
Amazon Simple Notification Service (SNS)
Engage	Firebase Remote Config	
Engage	Google Analytics	
Event handling	Eventarc	AWS EventBridge
Exfiltration prevention	VPC Service Controls	
FaaS	Cloud Functions	AWS Lambda
File storage	Filestore	Amazon Elastic File System (EFS)
Hardware security module (HSM)	Cloud HSM	AWS CloudHSM
IAM	Cloud Identity	AWS Identity Services
IAM	Identity and Access Management	Amazon Identity and Access Management
IAM	Managed Service for Microsoft Active Directory	AWS Managed Microsoft AD
In-memory data store	Memorystore	Amazon ElastiCache
Infrastructure modernization	SAP on Google Cloud	SAP on AWS
Infrequently accessed object storage	Cloud Storage Archive	Amazon S3 Glacier
IoT platform	Cloud IoT	AWS IoT Core
Kubernetes platform	Knative	AWS Fargate
Load balancer	Cloud Load Balancing	AWS Elastic Load Balancing
Logging	Cloud Logging	Amazon CloudWatch Logs
Marketplace	Marketplace	AWS Marketplace
Messaging	Pub/Sub	Amazon Simple Notification Service (SNS),
Amazon Simple Queueing Service (SQS)
Messaging	Pub/Sub Lite	Amazon Simple Notification Service,
Amazon Simple Queueing Service
ML for structured data	Vertex AI AutoML tabular models	Amazon SageMaker
ML platform	Vertex AI custom-trained models	Amazon SageMaker
ML platform	Vertex AI custom training	Amazon SageMaker
ML platform	Vertex AI AutoML models	Amazon SageMaker Autopilot
ML platform	Vertex AI	Amazon SageMaker
ML platform	Deep Learning VM Images	Amazon SageMaker, Amazon EC2 P3
ML platform	Vertex AI Workbench	Amazon SageMaker
ML platform	TensorFlow Enterprise	Tensorflow on AWS
Monitoring	Cloud Monitoring	Amazon CloudWatch
Multi-cloud	Anthos	AWS Outposts
Multi-cloud	Anthos attached clusters	
Multi-cloud	Anthos on bare metal	
Multi-cloud	Anthos clusters on AWS	
Multi-cloud	Anthos clusters on VMware	
Multi-cloud	Anthos Config Management	Chef Automate AWS OpsWorks
Multi-cloud	Config Connector	AWS Controllers for Kubernetes
Multi-cloud	Container-Optimized OS	
Multi-cloud	Hybrid Connectivity	AWS Direct Connect
Natural language processing	Natural Language AI	Amazon Comprehend
Network monitoring	Network Intelligence Center	
Network monitoring	VPC Flow Logs	Amazon VPC Flow Logs
Network security	Cloud VPN	AWS Virtual Private Network (VPN)
NoSQL: Indexed	Datastore	Amazon DynamoDB
NoSQL: Key-value	Cloud Bigtable	Amazon DynamoDB
Object storage	Cloud Storage	AWS Simple Storage Service (S3)
Open source processing	Dataproc	Amazon Elastic MapReduce (EMR),
AWS Batch,
AWS Glue
PaaS	App Engine	AWS Elastic Beanstalk
Performance tracing	Cloud Trace	AWS X-Ray
Personalization	Recommendations AI	Amazon Personalize
Premium networking	Network Service Tiers	
Profiling	Cloud Profiler	Amazon CodeGuru Profiler
Query service	BigQuery	Amazon Redshift Spectrum
RDBMS	Cloud Spanner	Amazon Aurora
RDBMS	Cloud SQL	Amazon Relational Database Service (RDS),
Amazon Aurora
Relational	Bare Metal Solution	Amazon RDS for Oracle
Release & monitor	Firebase App Distribution	
Release & monitor	Firebase Crashlytics	
Release & monitor	Firebase Performance Monitoring	
Release & monitor	Firebase Test Lab	AWS Device Farm
Resource monitoring	Cloud Asset Inventory	AWS Config
Resource monitoring	Resource Manager	AWS OpsWorks
Secret management	Secret Manager	AWS Secrets Manager
Security administration	Cloud Key Management Service	AWS Key Management Service (KMS)
Security and risk management	Security Command Center	Amazon Guard Duty, AWS Security Hub
Server migration	Migrate for Compute Engine	AWS Server Migration Service
Service mesh	Anthos Service Mesh	AWS App Mesh
Service mesh	Cloud Router	Amazon VPC
Transit Gateway
Service mesh	Istio on Google Kubernetes Engine	Istio on Amazon EKS
Service mesh	Traffic Director	AWS App Mesh
Service mesh	Traffic Director	AWS App Mesh
Services	Service Directory	AWS Cloud Map
SQL database migration	Database Migration Service	AWS Database Migration Service
Storage migration	Storage Transfer Service	AWS Storage Gateway
Storage migration	Transfer Appliance	AWS Snowball
Stream data ingest	Pub/Sub	Amazon Kinesis
Stream data processing	Dataflow	Amazon Kinesis
Streaming	Video Intelligence Streaming API	Live Streaming on AWS
Translation	Translation AI	Amazon Translate
Video intelligence	Video Intelligence API	Amazon Rekognition Video
Virtual networks	Cloud NAT	Amazon VPC NAT instances
Virtual networks	Virtual Private Cloud	Amazon Virtual Private Cloud (VPC)
Vision: Read and extract text	Vision AI	Amazon Textract
Vision: Speech-to-text	Speech-to-Text	Amazon Transcribe
VMware connectivity	VMware Engine	VMware Cloud on AWS
Web application firewall	Google Cloud Armor	AWS WAF
Workflow orchestration	Cloud Composer	Amazon Data Pipeline, AWS Glue,
Managed Workflows for Apache Air
Workflow orchestration	Workflows	AWS Step Functions
Zero trust	BeyondCorp Enterprise	


https://istio.io/latest/docs/tasks/observability/kiali/

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

## Anthos
- Anthos against kubernetes clusters on-prem, AWS, Azure

