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

## Q: 20220113: Evaluation Quota for top VM M2-megamem-416
...pending - details on a limited time eval of the performance of the following 416 vCore VM via https://cloud.google.com/compute/vm-instance-pricing
m2-megamem-416	416	5888GB	$50.372	Not available in this region	$30.387	$17.412

## Q: 20220113: Connecting to GCP Cloud SQL
https://cloud.google.com/sql/docs/mysql/quickstart-proxy-test#windows-64-bit

    in cloud shell
    michael@cloudshell:~ (biometric-335918)$ gcloud sql connect biometric --user=root --quiet
    Allowlisting your IP for incoming connection for 5 minutes...working...
    
    Add the role Cloud SQL Admin
    
    Enable Cloud SQL Admin API
    On the local machine - run the proxy
    PS C:\opt> ./cloud_sql_proxy -instances=biometric-335918:us-central1:biometric=tcp:3306
    2022/01/13 23:41:43 errors parsing config:
        googleapi: Error 403: The client is not authorized to make this request., notAuthorized
    
