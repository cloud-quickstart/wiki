# Solutions
- https://github.com/cloud-quickstart/wiki/issues/14
## Onboarding to GCP for Public Sector Organizations
- Base blog content - https://github.com/GoogleCloudPlatform/pbmm-on-gcp-onboarding/blob/main/docs/google-cloud-onboarding.md
- Multi-Organization Billing - https://github.com/GoogleCloudPlatform/pbmm-on-gcp-onboarding/blob/main/docs/google-cloud-onboarding.md#billing
- Blog
## KCC Landing Zone Deployment
- Base blog content - https://github.com/GoogleCloudPlatform/pubsec-declarative-toolkit/blob/dev/solutions/landing-zone/architecture.md
- Blog

## Implementing ITSG Security Controls in a GCP PBMM Landing Zone
- Base blog content - https://github.com/GoogleCloudPlatform/pbmm-on-gcp-onboarding/blob/main/docs/google-cloud-security-controls.md

## Example Canary/Workload for Dynamic Security Controls Compliance in GCP Landing Zones
- Base blog content - https://github.com/GoogleCloudPlatform/pbmm-on-gcp-onboarding/blob/main/docs/google-cloud-landingzone-traffic-generation.md
- Blog

## KCC Canary Deployments - IaaS
## KCC Canary Deployments - PaaS
## KCC Canary Deployments - FaaS
## KCC Canary Deployments - SaaS

## Fortinet/Fortigate NGFW use in GCP Secure Landing Zones
- Base blog content - https://github.com/GoogleCloudPlatform/pubsec-declarative-toolkit/blob/dev/solutions/landing-zone/architecture.md#fortigate-ha-active-standby-poc
- Blog


## Incorporate GCP Software Delivery Shield
- Base blog content - https://github.com/GoogleCloudPlatform/pubsec-declarative-toolkit/blob/dev/solutions/landing-zone/architecture.md#di-36-incorporate-software-delivery-shield
- 
## Training options for GCP
- base blog content - https://github.com/cloud-quickstart/wiki/blob/main/google-training.md
- Blog


# Developer Focused
- http://wiki.obrienlabs.cloud/display/DEV/Google
## Deploying Google Cloud Workstations in the GCP Landing Zone
- Base blog content - https://cloud.google.com/workstations
- Blog

## Using Google Cloud Deploy in a GCP Landing Zone for CI/CD Pipelines
- Base blog content - https://github.com/GoogleCloudPlatform/pubsec-declarative-toolkit/blob/dev/solutions/landing-zone/architecture.md#cloud-deploy-pipelines
- Base blog content - http://wiki.obrienlabs.cloud/display/DEV/Google+Cloud+Deploy
- Blog

## Heartrate/GPS IoT Streaming to Google Cloud
- https://github.com/cloud-quickstart/wiki/issues/16

- Base blog content - http://wiki.obrienlabs.cloud/display/DEV/Biometric+Dual+Heart+Rate+Streaming+from+Mobile+Devices
- Blog

### VPC 

```
gcloud compute networks create biometric --project=biometric-ol --description=biometric --subnet-mode=custom --mtu=1460 --bgp-routing-mode=regional

gcloud compute networks subnets create private --project=biometric-ol --range=10.0.0.0/24 --stack-type=IPV4_ONLY --network=biometric --region=us-central1 --enable-private-ip-google-access

```

Enable PSA - Private Services Access
https://cloud.google.com/vpc/docs/configure-private-services-access?_ga=2.179763492.-1098396564.1647194753

Cloud SQL Proxy
https://cloud.google.com/sql/docs/mysql/sql-proxy?_ga=2.150451510.-1098396564.1647194753

### Deploy a Bastion
https://console.cloud.google.com/compute/instancesAdd?walkthrough_id=sql--quickstart-sql-gce--quickstart-sql-gce-index&project=biometric-ol&supportedpurview=project
```
gcloud compute instances create bastion2 --project=biometric-ol --zone=us-central1-a --machine-type=e2-micro --network-interface=network-tier=PREMIUM,subnet=default --metadata=enable-oslogin=true --can-ip-forward --maintenance-policy=MIGRATE --provisioning-model=STANDARD --service-account=690900791045-compute@developer.gserviceaccount.com --scopes=https://www.googleapis.com/auth/cloud-platform --tags=http-server,https-server --create-disk=auto-delete=yes,boot=yes,device-name=bastion2,image=projects/debian-cloud/global/images/debian-11-bullseye-v20221102,mode=rw,size=10,type=projects/biometric-ol/zones/us-central1-a/diskTypes/pd-balanced --no-shielded-secure-boot --shielded-vtpm --shielded-integrity-monitoring --reservation-affinity=any
```

### Cloud SQL Migration

## Serverless Wiki/Websites on Google Cloud
- Base blog content - http://wiki.obrienlabs.cloud/display/DEV/Serverless+Websites+on+Google+Cloud
- Base blog content - https://github.com/cloud-quickstart/wiki/blob/main/google-cloud-static-website.md
- Blog


# Tutorials
## Hands-on: Deploy and Configure Anthos Service Mesh in Google Cloud
- https://github.com/cloud-quickstart/wiki/issues/13
## Hands-on: Create CI/CD Pipelines for Production and Development in Google Cloud
- https://github.com/cloud-quickstart/wiki/issues/12
## Hands-on: Use Migrate to Containers to containerize a VM and migrate the application to Anthos/GKE in Google Cloud
- https://github.com/cloud-quickstart/wiki/issues/11
