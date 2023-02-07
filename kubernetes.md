# Rancher
Rancher is an organization recently pruchased by SUSE that distributes Rancher and RKE.  I used Rancher since version 1.6 to deploy a kubernetes cluster across multiple nodes (physical and virtual).  RKE can be used at the command line for creating clusters like the one on 4 Intel NUCs at http://wiki.obrienlabs.cloud/display/DEV/Intel+NUC+Kubernetes+Cluster

## Installing Rancher on an OSX cluster using Suse Linux VMs
- Install VMware Fusion 13+ for a mix of intel and M1 chipsets
- create a Suse linux VM https://www.suse.com/shop/server/#subnav
- or an ubuntu 22.04 VM https://ubuntu.com/download/server/arm
- 

### RKE 1
- runs on docker - deprecated
### RKE 2 - RKE Government
- runs on containerd
- higher security (FIPS) and control plane abstraction away from Docker
- https://www.suse.com/c/rancher_blog/rke-vs-rke2-comparing-kubernetes-distros/
- https://docs.rke2.io/
### K3S
- half the memory footprint for embedded devices

# Google Kubernetes Engine
# Contributing to Kubernetes
https://github.com/kubernetes/community/blob/master/contributors/guide/README.md

Google Cloud Deployment Manager exports to Kubernetes Resource Model or Terraform - https://cloud.google.com/deployment-manager/docs/dm-convert?_ga=2.245568516.-1453179973.1650887889

# Links
- Kiali - Consol for ISTIO Service Mesh - https://kiali.io/docs/installation/quick-start/
- http://wiki.obrienlabs.cloud/display/DEV/Kubernetes+Developer+Guide
