# FAQ
## Q: 20220113: Cloud Run stop/start behaviour during request restarts
How does cloud run handle a shutdown container that starts to experience traffic after a prolonged quiet period
Cloud run offers a SIGTERM for up to 10s on shutdown


[Cloud Deployment Manager / Terraform templates for Google Cloud](https://cloud.google.com/foundation-toolkit/)

[Google Cloud gcloud CLI Cheatsheet](https://cloud.google.com/sdk/docs/cheatsheet)

## Q: 20220113: Quota increases for large VMs
New accounts should have no issues getting up to 96 vCPUs via the following quota limit changes which normally take 2-4 min of a 2d max wait time.  Quotas of 112, 128, 224 will need some account history.

https://console.cloud.google.com/iam-admin/quotas

    CPUS_ALL_REGIONS GLOBAL   96    
    N2D_CPUS  us-central1      96   
    
    
    michael@spot:~$ lscpu
    Architecture:        x86_64
    CPU op-mode(s):      32-bit, 64-bit
    Byte Order:          Little Endian
    Address sizes:       48 bits physical, 48 bits virtual
    CPU(s):              96
