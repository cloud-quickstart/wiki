# References
- Obrienlabs Dev Blog - https://github.com/ObrienlabsDev/blog/wiki
- Historical - Obrienlabs Blogspot - https://eclipsejpa.blogspot.com/
- 

# Wiki / Confluence site

[cloud-guardrails](https://github.com/cloud-quickstart/wiki/blob/main/cloud-guardrails.md)

[cloud-services-grid](https://github.com/cloud-quickstart/wiki/blob/main/cloud-services-grid.md)

[google-cloud-certification](https://github.com/cloud-quickstart/wiki/blob/main/google-cloud-certification.md)

[google-cloud-onboarding](https://github.com/cloud-quickstart/wiki/blob/main/google-cloud-onboarding.md)

# Google Cloud Platform
[Google Cloud Whats new](https://cloud.google.com/blog/topics/inside-google-cloud/whats-new-google-cloud) | 
## Developer Setup
### Installing the Google Cloud SDK
- https://github.com/cloud-quickstart/gcp-landing-zone (GCP Java SDK in progress)

### Installing the Google Cloud SDK on Windows

https://cloud.google.com/sdk/docs/cheatsheet

#### Issue: python version error running gcloud
There are currently issues with Python 3.10+ running gcloud as of 20211121.  The temporary fix is to revert to Python 3.7 or 2.7.
After switching the following environment varable to point to an older python installation and rerunning the shell (ming64 in this case) we are good

    Before
    
    $ gcloud config list
    
    $ gcloud version
    ERROR: gcloud failed to load: module 'collections' has no attribute 'Mapping'
    gcloud_main = _import_gcloud_main()
    import googlecloudsdk.gcloud_main
    from googlecloudsdk.calliope import cli
    from googlecloudsdk.calliope import actions
    from googlecloudsdk.calliope import markdown
    from googlecloudsdk.calliope import usage_text
    from googlecloudsdk.calliope import parser_arguments
    from googlecloudsdk.calliope import parser_completer
    from googlecloudsdk.core.console import progress_tracker
    class _BaseStagedProgressTracker(collections.Mapping):

    This usually indicates corruption in your gcloud installation or problems with your Python interpreter.

    Please verify that the following is the path to a working Python 2.7 or 3.5+ executable:
    C:\opt\python3\python.exe

    If it is not, please set the CLOUDSDK_PYTHON environment variable to point to a working Python 2.7 or 3.5+ executable.

    
    After
    MINGW64 ~
    $ gcloud version
    Google Cloud SDK 365.0.0
    bq 2.0.71
    core 2021.11.12
    gsutil 5.5


### Installing the Google Cloud SDK on a bastion/jump box

#### Create GCP VM

    Linux biometric 4.19.0-18-cloud-amd64 #1 SMP Debian 4.19.208-1 (2021-09-29) x86_64
    
    Ask for quota increase - usually 1-3 min not 48h
    https://console.cloud.google.com/iam-admin/quotas?referrer=search&project=biometric-335918&pageState=(%22allQuotasTable%22:(%22f%22:%22%255B%257B_22k_22_3A_22_22_2C_22t_22_3A10_2C_22v_22_3A_22_5C_22N2D_CPUS_5C_22_22%257D_2C%257B_22k_22_3A_22_22_2C_22t_22_3A10_2C_22v_22_3A_22_5C_22us-central1_5C_22_22%257D%255D%22,%22p%22:0))

    +------------------+-------------+-----------------+
    |       Name       |    Region   | Requested Limit |
    +------------------+-------------+-----------------+
    | PREEMPTIBLE_CPUS | us-central1 |        96       |
    |     C2_CPUS      | us-central1 |        96       |
    |     N2D_CPUS     | us-central1 |        96       |
    | COMMITTED_N2D_CPUS | us-central1 |        96       |
    | CPUS_ALL_REGIONS |    GLOBAL   |        96       |
    | CPUS_ALL_REGIONS |    GLOBAL   |       112       |
    +------------------+-------------+-----------------+
    
    michael@spot:~$ lscpu
    Architecture:        x86_64
    CPU op-mode(s):      32-bit, 64-bit
    Byte Order:          Little Endian
    Address sizes:       48 bits physical, 48 bits virtual
    CPU(s):              96
    On-line CPU(s) list: 0-95
    Thread(s) per core:  2
    Core(s) per socket:  24
    Socket(s):           2
    NUMA node(s):        2
    Vendor ID:           AuthenticAMD
    CPU family:          23
    Model:               49
    Model name:          AMD EPYC 7B12
    Stepping:            0
    CPU MHz:             2249.996
    BogoMIPS:            4499.99
    Hypervisor vendor:   KVM
    Virtualization type: full
    L1d cache:           32K
    L1i cache:           32K
    L2 cache:            512K
    L3 cache:            16384K
    NUMA node0 CPU(s):   0-23,48-71
    NUMA node1 CPU(s):   24-47,72-95

    for m2-ultramem-208 (5.75) $38 hourly

    for containerized.org
    Thank you for submitting Case # (ID:82174b6e1fca4e3188023998adc5e9b3) to Google Cloud Platform support for the following quota:
		Change CPUs - us-central1 from 24 to 128

    Your quota request for biometric-dev has been partially approved and your
    project quota has been adjusted according to the following requested limits:

    +------+-------------+-----------------+
    | Name |    Region   | Requested Limit |
    +------+-------------+-----------------+
    | CPUS | us-central1 |       128       |
    +------+-------------+-----------------+

    Unfortunately, we were unable to grant your below quota request(s):

    +------------------+--------+
    |       Name       | Region |
    +------------------+--------+
    | CPUS_ALL_REGIONS | GLOBAL |
    +------------------+--------+

    Operation type [insert] failed with message "Quota 'CPUS_ALL_REGIONS' exceeded. Limit: 32.0 globally."

    Create spot VM
    michael@cloudshell:~ (biometric-335918)$ gcloud beta compute instances create biometric-spot --provisioning-model=SPOT --zone us-central1-b
    Created [https://www.googleapis.com/compute/beta/projects/biometric-335918/zones/us-central1-b/instances/biometric-spot].
    NAME: biometric-spot
    ZONE: us-central1-b
    MACHINE_TYPE: n1-standard-1
    PREEMPTIBLE: true
    INTERNAL_IP: 10.128.0.2
    EXTERNAL_IP: 34...80
    STATUS: RUNNING
    using preemptible quota
    
    Linux biometric 4.19.0-18-cloud-amd64 #1 SMP Debian 4.19.208-1 (2021-09-29) x86_64
    michael@biometric:~$ gcloud --version
    Google Cloud SDK 366.0.0
    alpha 2021.12.03
    beta 2021.12.03
    bq 2.0.72
    core 2021.12.03
    gsutil 5.5
    
    Welcome to Ubuntu 18.04.6 LTS (GNU/Linux 5.4.0-1059-gcp x86_64)
    michael@services:~$ gcloud version
    Google Cloud SDK 372.0.0
    alpha 2022.02.04
    beta 2022.02.04
    bq 2.0.73
    core 2022.02.04
    gsutil 5.6
    minikube 1.24.0
    skaffold 1.35.1
    
    michael@services:~$ gcloud auth list
                  Credentialed Accounts
    ACTIVE  ACCOUNT
    *       2.....2-compute@developer.gserviceaccount.com

    michael@services:~$ gcloud config set account 2..-compute@developer.gserviceaccount.com
    Updated property [core/account].
    michael@services:~$ gcloud compute instances list
    NAME       ZONE           MACHINE_TYPE   PREEMPTIBLE  INTERNAL_IP  EXTERNAL_IP     STATUS
    biometric  us-central1-a  e2-micro                    10.128.0.4   34..22   RUNNING
    services   us-east4-c     n1-standard-2               10.150.0.2   34..18  RUNNING

#### Run collatz to benchmark the VM

http://wiki.obrienlabs.cloud/display/DEV/Performance#Performance-FullKubernetesClusterCPUSaturation

    sudo apt update
    sudo apt upgrade
    sudo apt-get install curl
    sudo curl https://releases.rancher.com/install-docker/19.03.sh | sh
    sudo usermod -aG docker michael
    sudo docker run --name collatz -d obrienlabs/collatz-se:0.0.1
    sudo docker logs collatz -f


    michael@hpe1:~$ sudo docker logs collatz -f
    ForkJoinCollatzServer forkJoinPool-power-start end runs (v 20161009)
    availableProc   : 60
    fjps threads    : 5,6
    freeMemory()    : 2143287296
    maxMemory()     : 32178700288
    totalMemory()   : 2147483648
    System.getEnv() : {PATH=/usr/local/openjdk-11/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin, HOSTNAME=74761e04c44f, JAVA_HOME=/usr/local/openjdk-11, OLDPWD=/, JAVA_VERSION=11.0.8, PWD=/opt/app, LANG=C.UTF-8, SHLVL=1, HOME=/root, _=/usr/local/openjdk-11/bin/java}
    Range: bits     : 25
    5246,5,22,522,8
    4338,5,21,421,16
    4310,5,20,420,32
    4320,5,19,419,64
    4279,5,18,418,128
    4296,5,17,417,256
    4212,5,16,416,512
    4333,5,15,415,1024
    4262,5,14,414,2048
    4266,5,13,413,4096
    4264,5,12,412,8192
    4361,5,11,411,16384
    4286,5,10,410,32768
    4344,5,9,49,65536
    4378,5,8,48,131072
    4525,5,7,47,262144
    4734,5,6,46,524288
    5136,5,5,55,1048576
    5504,5,4,54,2097152
    9688,5,3,93,4194304
    19134,5,2,192,8388608
    36621,5,1,361,16777216
    69954,5,0,690,33554432



### Installing the Google Cloud SDK on osx

https://cloud.google.com/sdk/docs/quickstart

    biometric:google-cloud-sdk $ ./install.sh
    Welcome to the Google Cloud SDK!
    
    │     Status    │                         Name                         │            ID            │   Size   │
    ├───────────────┼──────────────────────────────────────────────────────┼──────────────────────────┼──────────┤
    │ Not Installed │ App Engine Go Extensions                             │ app-engine-go            │  4.8 MiB │
    │ Not Installed │ Appctl                                               │ appctl                   │ 18.5 MiB │
    │ Not Installed │ Cloud Bigtable Command Line Tool                     │ cbt                      │  7.6 MiB │
    │ Not Installed │ Cloud Bigtable Emulator                              │ bigtable                 │  6.6 MiB │
    │ Not Installed │ Cloud Datalab Command Line Tool                      │ datalab                  │  < 1 MiB │
    │ Not Installed │ Cloud Datastore Emulator                             │ cloud-datastore-emulator │ 18.4 MiB │
    │ Not Installed │ Cloud Firestore Emulator                             │ cloud-firestore-emulator │ 40.5 MiB │
    │ Not Installed │ Cloud Pub/Sub Emulator                               │ pubsub-emulator          │ 60.7 MiB │
    │ Not Installed │ Cloud SQL Proxy                                      │ cloud_sql_proxy          │  7.4 MiB │
    │ Not Installed │ Emulator Reverse Proxy                               │ emulator-reverse-proxy   │ 14.5 MiB │
    │ Not Installed │ Google Cloud Build Local Builder                     │ cloud-build-local        │  6.2 MiB │    
    │ Not Installed │ Google Container Registry's Docker credential helper │ docker-credential-gcr    │  2.2 MiB │
    │ Not Installed │ Kustomize                                            │ kustomize                │  7.6 MiB │
    │ Not Installed │ Minikube                                             │ minikube                 │ 26.6 MiB │
    │ Not Installed │ Nomos CLI                                            │ nomos                    │ 24.4 MiB │
    │ Not Installed │ On-Demand Scanning API extraction helper             │ local-extract            │ 12.5 MiB │
    │ Not Installed │ Skaffold                                             │ skaffold                 │ 20.1 MiB │
    │ Not Installed │ anthos-auth                                          │ anthos-auth              │ 18.0 MiB │
    │ Not Installed │ config-connector                                     │ config-connector         │ 47.6 MiB │
    │ Not Installed │ gcloud Alpha Commands                                │ alpha                    │  < 1 MiB │
    │ Not Installed │ gcloud Beta Commands                                 │ beta                     │  < 1 MiB │
    │ Not Installed │ gcloud app Java Extensions                           │ app-engine-java          │ 51.7 MiB │
    │ Not Installed │ gcloud app PHP Extensions                            │ app-engine-php           │ 21.9 MiB │
    │ Not Installed │ gcloud app Python Extensions                         │ app-engine-python        │  7.8 MiB │
    │ Not Installed │ gcloud app Python Extensions (Extra Libraries)       │ app-engine-python-extras │ 26.4 MiB │
    │ Not Installed │ kpt                                                  │ kpt                      │ 12.9 MiB │
    │ Not Installed │ kubectl                                              │ kubectl                  │  < 1 MiB │
    │ Not Installed │ kubectl-oidc                                         │ kubectl-oidc             │ 18.0 MiB │
    │ Not Installed │ pkg                                                  │ pkg                      │          │
    │ Installed     │ BigQuery Command Line Tool                           │ bq                       │  < 1 MiB │
    │ Installed     │ Cloud SDK Core Libraries                             │ core                     │ 21.2 MiB │
    │ Installed     │ Cloud Storage Command Line Tool                      │ gsutil                   │  8.1 MiB │
    └───────────────┴──────────────────────────────────────────────────────┴──────────────────────────┴──────────┘
    To install or remove components at your current SDK version [365.0.0], run:
      $ gcloud components install COMPONENT_ID
      $ gcloud components remove COMPONENT_ID

    To update your SDK installation to the latest version [365.0.0], run:
      $ gcloud components update
          
      Enter a path to an rc file to update, or leave blank to use [/Users//.zshrc]:  /Users//.bash_profile

      already have python 3.9 - you must run the 3.7 installer
      Cloud SDK works best with Python 3.7 and certain modules.
    Download and run Python 3.7 installer? (Y/n)?  y
    Running Python 3.7 installer, you may be prompted for sudo password...
    Password:
    installer: Package name is Python
    installer: Upgrading at base path /
    installer: The upgrade was successful.
    Setting up virtual environment
    Creating virtualenv...
    Installing modules...
     |████████████████████████████████| 118 kB 46.2 MB/s 
    Running setup.py install for crcmod ... done
    Virtual env enabled.

    verify....
    biometric:google-cloud-sdk$ source ~/.bash_profile
    biometric:google-cloud-sdk $ gcloud version
    Google Cloud SDK 365.0.0
    bq 2.0.71
    core 2021.11.12
    gsutil 5.5

## Google Cloud Shell

## Authenticating local CLI access

https://cloud.google.com/sdk/docs/authorizing

Use '''gcloud init''' and accept the option to authenticate a new account

Pick cloud project to use:
 [1] biometric-334503
 [2] thermal-slice-332322
 [3] Create a new project
Please enter numeric choice or text value (must exactly match list item):  1

Your current project has been set to: [biometric-334503].

Not setting default zone/region (this feature makes it easier to use
[gcloud compute] by setting an appropriate default value for the
--zone and --region flag).
See https://cloud.google.com/compute/docs/gcloud-compute section on how to set
default compute region and zone manually. If you would like [gcloud init] to be
able to do this for you the next time you run it, make sure the
Compute Engine API is enabled for your project on the
https://console.developers.google.com/apis page.

Your Google Cloud SDK is configured and ready to use!

* Commands that require authentication will use m by default
* Commands will reference project `biometric-334503` by default
Run `gcloud help config` to learn how to change individual settings

This gcloud configuration is called [obrienlabs-cloud]. You can create additional configurations if you work with multiple accounts and/or projects.
Run `gcloud topic configurations` to learn more.

Some things to try next:

* Run `gcloud --help` to see the Cloud Platform services you can interact with. And run `gcloud help COMMAND` to get help on any gcloud command.
* Run `gcloud topic --help` to learn about advanced features of the SDK like arg files and output formatting


gcloud auth list
gcloud config list project


## gcloud shell configuration
### Changing to Java 17 from 11 in the shell
### Configuring github credentials 
```
michael@cloudshell:~$ git config --global user.email ""
michael@cloudshell:~$ git config --global user.name "Michael "
```
### Using a service account

# Google Kubernetes Engine - GKE
## GKE Quickstart

https://cloud.google.com/kubernetes-engine/docs/quickstart

### Reconnecting to the GKE cluster

Reconnect the google cloud shell

    Welcome to Cloud Shell! Type "help" to get started.
    Your Cloud Platform project in this session is set to biometric-334301.
    Use “gcloud config set project [PROJECT_ID]” to change to a different project.
    
    fmobrien9@cloudshell:~ (biometric-334301)$ gcloud container clusters get-credentials cluster1 --zone us-central1-c --project biometric-334301
    Fetching cluster endpoint and auth data.
    kubeconfig entry generated for cluster1.
    fmobrien9@cloudshell:~ (biometric-334301)$ kubectl get nodes
    NAME                                      STATUS   ROLES    AGE   VERSION
    gke-cluster1-default-pool-c3afce1b-05ll   Ready    <none>   12h   v1.21.5-gke.1302
    gke-cluster1-default-pool-c3afce1b-7cn9   Ready    <none>   12h   v1.21.5-gke.1302
    gke-cluster1-default-pool-c3afce1b-lx3w   Ready    <none>   12h   v1.21.5-gke.1302
    gke-cluster1-default-pool-c3afce1b-nqzq   Ready    <none>   12h   v1.21.5-gke.1302

## Google Compute

    PS C:\Windows\system32> gcloud compute instances list
    API [compute.googleapis.com] not enabled on project [991698271966]. Would you like to enable and retry (this will take a few minutes)? (y/N)?  y
    Enabling service [compute.googleapis.com] on project [991698271966]...

# Terraform on Google Cloud
## Terraform is provisioned with Google Cloud Shell
Use an example https://registry.terraform.io/modules/terraform-google-modules/kubernetes-engine/google/latest

https://www.hashicorp.com/blog/kickstart-terraform-on-gcp-with-google-cloud-shell

https://registry.terraform.io/providers/hashicorp/google/latest/docs


    Welcome to Cloud Shell! Type "help" to get started.
    To set your Cloud Platform project in this session use “gcloud config set project [PROJECT_ID]”
    cloudshell_open --repo_url "https://github.com/terraform-google-modules/docs-examples.git" --print_file "./motd" --dir "address_basic" --page "editor" --tutorial "./tutorial.md" --open_in_editor "main.tf" --force_new_clone
    michael@cloudshell:~$ cloudshell_open --repo_url "https://github.com/terraform-google-modules/docs-examples.git" --print_file "./motd" --dir "address_basic" --page "editor" --tutorial "./tutorial.md" --open_in_editor "main.tf" --force_new_clone
    2021/12/16 03:08:42 Cloning https://github.com/terraform-google-modules/docs-examples.git into /home/michael/cloudshell_open/docs-examples
    Cloning into '/home/michael/cloudshell_open/docs-examples'...
    remote: Enumerating objects: 1906, done.
    remote: Total 1906 (delta 0), reused 0 (delta 0), pack-reused 1906
    Receiving objects: 100% (1906/1906), 447.94 KiB | 7.46 MiB/s, done.
    Resolving deltas: 100% (1442/1442), done.
    2021/12/16 03:08:43 ===
 

    ===
    michael@cloudshell:~/cloudshell_open/docs-examples/address_basic$ ls
    backing_file.tf  main.tf  motd  tutorial.md
    michael@cloudshell:~/cloudshell_open/docs-examples/address_basic$ export GOOGLE_CLOUD_PROJECT=dev-sphere-335220
    michael@cloudshell:~/cloudshell_open/docs-examples/address_basic$ terraform init
    
    Initializing provider plugins...
    - Finding latest version of hashicorp/google...
    - Finding latest version of hashicorp/random...
    - Installing hashicorp/google v4.4.0...
    - Installed hashicorp/google v4.4.0 (self-signed, key ID 34365D9472D7468F)
    - Installing hashicorp/random v3.1.0...
    - Installed hashicorp/random v3.1.0 (self-signed, key ID 34365D9472D7468F)

    Terraform has created a lock file .terraform.lock.hcl to record the provider
    selections it made above. Include this file in your version control repository
    so that Terraform can guarantee to make the same selections by default when
    you run "terraform init" in the future.

    Terraform has been successfully initialized!

    You may now begin working with Terraform. Try running "terraform plan" to see
    any changes that are required for your infrastructure. All Terraform commands
    should now work.

    If you ever set or change modules or backend configuration for Terraform,
    rerun this command to reinitialize your working directory. If you forget, other
    commands will detect it and remind you to do so if necessary.
 
    │ Error: Error creating Address: googleapi: Error 403: Compute Engine API has not been used in project 313394869326 before or it is disabled. Enable it by visiting https://console.developers.google.com/apis/api/compute.googleapis.com/overview?project=313394869326 then retry. If you enabled this API recently, wait a few minutes for the action to propagate to our systems and retry.
    │ Details:
    │ [
    │   {
    │     "@type": "type.googleapis.com/google.rpc.Help",
    │     "links": [
    │       {
    │         "description": "Google developers console API activation",
    │         "url": "https://console.developers.google.com/apis/api/compute.googleapis.com/overview?project=313394869326"
    │       }
    │     ]
    │   },
    │   {
    │     "@type": "type.googleapis.com/google.rpc.ErrorInfo",
    │     "domain": "googleapis.com",
    │     "metadata": {
    │       "consumer": "projects/313394869326",
    │       "service": "compute.googleapis.com"
    │     },
    │     "reason": "SERVICE_DISABLED"
    │   }
    │ ]
    │ , accessNotConfigured
    │
    │   on main.tf line 1, in resource "google_compute_address" "ip_address":
    │    1: resource "google_compute_address" "ip_address" {
 
    Forgot to enable compute - run...
 
    michael@cloudshell:~/cloudshell_open/docs-examples/address_basic$ gcloud config set project dev-sphere-335220
    Updated property [core/project].
    michael@cloudshell:~/cloudshell_open/docs-examples/address_basic (dev-sphere-335220)$ gcloud services enable compute.googleapis.com
 
    terraform apply
 
    google_compute_address.ip_address: Creating...
    google_compute_address.ip_address: Still creating... [10s elapsed]
    google_compute_address.ip_address: Creation complete after 13s [id=projects/dev-sphere-335220/regions/us-central1/addresses/my-address-one-doberman]
 
    Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
 
     michael@cloudshell:~/cloudshell_open/docs-examples/address_basic (dev-sphere-335220)$ cat terraform.tfstate
    {
      "version": 4,
      "terraform_version": "0.15.0",
      "serial": 9,
      "lineage": "15b70e84-53ce-6cf7-3518-ed294a4181d2",
      "outputs": {},
      "resources": [
        {
          "mode": "managed",
          "type": "google_compute_address",
          "name": "ip_address",
          "provider": "provider[\"registry.terraform.io/hashicorp/google\"]",
          "instances": [
            {
              "schema_version": 0,
              "attributes": {
                "address": "34.70.49.6",
                "address_type": "EXTERNAL",
                "creation_timestamp": "2021-12-15T19:40:55.884-08:00",
                "description": "",
                "id": "projects/dev-sphere-335220/regions/us-central1/addresses/my-address-ample-spaniel",
                "name": "my-address-ample-spaniel",
                "network": "",
                "network_tier": "PREMIUM",
                "prefix_length": 0,
                "project": "dev-sphere-335220",
                "purpose": "",
                "region": "us-central1",
                "self_link": "https://www.googleapis.com/compute/v1/projects/dev-sphere-335220/regions/us-central1/addresses/my-address-ample-spaniel",
                "subnetwork": "",
                "timeouts": null,
                "users": []
              },
              "sensitive_attributes": [],
              "private": "eyJlMmJmYjczMC1lY2FhLTExZTYtOGY4OC0zNDM2M2JjN2M0YzAiOnsiY3JlYXRlIjoyNDAwMDAwMDAwMDAsImRlbGV0ZSI6MjQwMDAwMDAwMDAwfX0=",
              "dependencies": [
                "random_pet.suffix"
              ]
            }
          ]
        },
        {
          "mode": "managed",
          "type": "random_pet",
          "name": "suffix",
          "provider": "provider[\"registry.terraform.io/hashicorp/random\"]",
          "instances": [
            {
              "schema_version": 0,
              "attributes": {
                "id": "ample-spaniel",
                "keepers": null,
                "length": 2,
                "prefix": null,
                "separator": "-"
              },
              "sensitive_attributes": [],
              "private": "bnVsbA=="
             }
          ]
        }
      ]
    }

    terraform destroy
    google_compute_address.ip_address: Destroying... [id=projects/dev-sphere-335220/regions/us-central1/addresses/my-address-one-doberman]
    google_compute_address.ip_address: Still destroying... [id=projects/dev-sphere-335220/regions/us-central1/addresses/my-address-one-doberman, 10s elapsed]
    google_compute_address.ip_address: Destruction complete after 11s

    random_pet.suffix: Destroying... [id=one-doberman]
    random_pet.suffix: Destruction complete after 0s
 
    Destroy complete! Resources: 2 destroyed.

    michael@cloudshell:~/cloudshell_open/docs-examples/address_basic (dev-sphere-335220)$ cat terraform.tfstate    
    {
      "version": 4,
      "terraform_version": "0.15.0",
      "serial": 6,
      "lineage": "15b70e84-53ce-6cf7-3518-ed294a4181d2",
      "outputs": {},
      "resources": [] 
    }

## Old School - GCE via CLI with docker

michael@services:~$ gcloud version
Google Cloud SDK 367.0.0
alpha 2021.12.10
beta 2021.12.10
bq 2.0.72
core 2021.12.10
gsutil 5.5
minikube 1.24.0
skaffold 1.34.0


michael@cloudshell:~ (biometric-335918)$ gcloud compute zones list | grep us-east4
NAME: us-east4-c
REGION: us-east4
NAME: us-east4-b
REGION: us-east4
NAME: us-east4-a
REGION: us-east4
michael@cloudshell:~ (biometric-335918)$ gcloud config set compute/zone us-east4-c
Updated property [compute/zone].


 sudo apt update
 sudo apt upgrade
 sudo apt-get install curl

 sudo curl https://releases.rancher.com/install-docker/20.10.sh | sh
 sudo usermod -aG docker mich

ichael@services:~$ sudo docker run --name reference-nbi -d -p 8888:8080 obrienlabs/reference-nbi:0.0.1
Unable to find image 'obrienlabs/reference-nbi:0.0.1' locally
0.0.1: Pulling from obrienlabs/reference-nbi
c67289558ae5: Pull complete 
12787f1f3888: Pull complete 
33b68cfe81ae: Extracting [=============================>                     ]  110.9MB/187.1MB
01504f33d5ce: Download complete 
ee05f50557f5: Download complete 


michael@services:~$ curl http://127.0.0.1:8888/nbi/api
{"id":1,"content":"1 PASS cloud.containerization.reference.nbi.ApiController URL: http://127.0.0.1:8888/nbi/api URI: /nbi/api path: null referer: null caller: null Host: 127.0.0.1:8888 queryString: null decodedQueryString: null secret1: null secret2: /root username: null session attributes:  :  remoteAddr: 172.17.0.1 localAddr: 172.17.0.2 remoteHost: 172.17.0.1 serverName: 127.0.0.1"}

michael@services:~$ sudo docker stop reference-nbi
reference-nbi
michael@services:~$ sudo docker rm reference-nbi
reference-nbi
michael@services:~$ sudo docker run --name reference-nbi -d -p 80:8080 obrienlabs/reference-nbi:0.0.1
8893088a1771253e5e244c897e350e3f22316e2705872ff52d7b2d6ff37070c9


# CI/CD



cloudshell_open --repo_url "https://github.com/GoogleCloudPlatform/spinnaker-for-gcp.git" --print_file "instructions.txt" --dir "scripts/install" --page "editor" --tutorial "provision-spinnaker.md" --force_new_clone
Welcome to Cloud Shell! Type "help" to get started.
To set your Cloud Platform project in this session use “gcloud config set project [PROJECT_ID]”
michael@cloudshell:~$ cloudshell_open --repo_url "https://github.com/GoogleCloudPlatform/spinnaker-for-gcp.git" --print_file "instructions.txt" --dir "scripts/install" --page "editor" --tutorial "provision-spinnaker.md" --force_new_clone
2022/02/09 15:13:39 Cloning https://github.com/GoogleCloudPlatform/spinnaker-for-gcp.git into /home/michael/cloudshell_open/spinnaker-for-gcp
Cloning into '/home/michael/cloudshell_open/spinnaker-for-gcp'...
remote: Enumerating objects: 1113, done.
remote: Counting objects: 100% (56/56), done.
remote: Compressing objects: 100% (45/45), done.
remote: Total 1113 (delta 29), reused 23 (delta 11), pack-reused 1057
Receiving objects: 100% (1113/1113), 609.03 KiB | 11.28 MiB/s, done.
Resolving deltas: 100% (714/714), done.
2022/02/09 15:13:40
+-------------------------------------------------------------------------------------------------------+
|                                                                                                       |
| To reopen the installation instructions in the right-hand pane at any time, enter:                    |
|                                                                                                       |
| cloudshell launch-tutorial ~/cloudshell_open/spinnaker-for-gcp/scripts/install/provision-spinnaker.md |
|                                                                                                       |
+-------------------------------------------------------------------------------------------------------+

michael@cloudshell:~/cloudshell_open/spinnaker-for-gcp/scripts/install$ git config --global user.email "mi..rg"
michael@cloudshell:~/cloudshell_open/spinnaker-for-gcp/scripts/install$ git config --global user.name "Michael OBrien"
michael@cloudshell:~/cloudshell_open/spinnaker-for-gcp/scripts/install$ git config --global user.email "mi..rg"
michael@cloudshell:~/cloudshell_open/spinnaker-for-gcp/scripts/install$ PROJECT_ID=biometric-dev \
>     ~/cloudshell_open/spinnaker-for-gcp/scripts/install/setup_properties.sh
michael@cloudshell:~/cloudshell_open/spinnaker-for-gcp/scripts/install$ cloudshell edit \
>     ~/cloudshell_open/spinnaker-for-gcp/scripts/install/properties
michael@cloudshell:~/cloudshell_open/spinnaker-for-gcp/scripts/install$ ~/cloudshell_open/spinnaker-for-gcp/scripts/install/setup.sh
Updated property [core/project].
.  Your Spinnaker config references GCP project id biometric-dev, but your gcloud default project id was not set. 
.  For safety when executing gcloud commands, 'gcloud config set project biometric-dev' has been used to change the gcloud default. 
.  Enabling required APIs (cloudbuild.googleapis.com cloudfunctions.googleapis.com container.googleapis.com endpoints.googleapis.com iap.googleapis.com monitoring.googleapis.com redis.googleapis.com sourcerepo.googleapis.com) in biometric-dev... 
.  This phase will take a few minutes (progress will not be reported during this operation). 
.   
.  Once the required APIs are enabled, the remaining components will be installed and configured. The entire installation may take 10 minutes or more. 
Operation "operations/acf.p2-40440447981-f2b902ce-ce2c-493f-b7c9-5a8218397b4d" finished successfully.
.  Checking for existing cluster spinnaker-1... 
WARNING: The following filter keys were not present in any resource : name
.  Creating service account spinnaker-1-acc-1644420526... 
Created service account [spinnaker-1-acc-1644420526].
.  Assigning required roles to spinnaker-1-acc-1644420526... 
.  Assigning role cloudbuild.builds.editor... 
Updated IAM policy for project [biometric-dev].
.  Assigning role container.admin... 
Updated IAM policy for project [biometric-dev].
.  Assigning role logging.logWriter... 
Updated IAM policy for project [biometric-dev].
.  Assigning role monitoring.admin... 
Updated IAM policy for project [biometric-dev].
.  Assigning role pubsub.admin... 
Updated IAM policy for project [biometric-dev].
.  Assigning role storage.admin... 
Updated IAM policy for project [biometric-dev].
WARNING: The following filter keys were not present in any resource : name
.  Creating redis instance spinnaker-1 in project biometric-dev... 
Create request issued for: [spinnaker-1]
Waiting for operation [projects/biometric-dev/locations/us-east1/operations/operation-1644420716398-5d79788a98994-57e91627-8aa040ae] to complete...done.     
Created instance [spinnaker-1].
BucketNotFoundException: 404 gs://spinnaker-1-93vhlkx30b5bqehl87fp-1644420526 bucket does not exist.
.  Creating bucket gs://spinnaker-1-93vhlkx30b5bqehl87fp-1644420526... 
Creating gs://spinnaker-1-93vhlkx30b5bqehl87fp-1644420526/...
Enabling versioning for gs://spinnaker-1-93vhlkx30b5bqehl87fp-1644420526/...
.  Creating GKE cluster spinnaker-1... 
WARNING: The `--enable-stackdriver-kubernetes` flag is deprecated and will be removed in an upcoming release. Please use `--logging` and `--monitoring` instead. For more information, please read: https://cloud.google.com/stackdriver/docs/solutions/gke/installing.
Note: The Pod address range limits the maximum size of the cluster. Please refer to https://cloud.google.com/kubernetes-engine/docs/how-to/flexible-pod-cidr to learn how to optimize IP address allocation.

Creating cluster spinnaker-1 in us-east1-c...done.     
Created [https://container.googleapis.com/v1beta1/projects/biometric-dev/zones/us-east1-c/clusters/spinnaker-1].
To inspect the contents of your cluster, go to: https://console.cloud.google.com/kubernetes/workload_/gcloud/us-east1-c/spinnaker-1?project=biometric-dev
kubeconfig entry generated for spinnaker-1.
NAME: spinnaker-1
LOCATION: us-east1-c
MASTER_VERSION: 1.20.12-gke.1500
MASTER_IP: 35.243.148.71
MACHINE_TYPE: n1-highmem-4
NODE_VERSION: 1.20.12-gke.1500
NUM_NODES: 3
STATUS: RUNNING
.  Retrieving credentials for GKE cluster spinnaker-1... 
Fetching cluster endpoint and auth data.
kubeconfig entry generated for spinnaker-1.
WARNING: The following filter keys were not present in any resource : name
.  Creating pubsub topic projects/biometric-dev/topics/gcr for GCR... 
Created topic [projects/biometric-dev/topics/gcr].
WARNING: The following filter keys were not present in any resource : name
.  Creating pubsub subscription spinnaker-1-gcr-pubsub-subscription for GCR... 
Created subscription [projects/biometric-dev/subscriptions/spinnaker-1-gcr-pubsub-subscription].
.  Creating pubsub topic projects/biometric-dev/topics/cloud-builds for GCB... 
Created topic [projects/biometric-dev/topics/cloud-builds].
.  Creating pubsub subscription spinnaker-1-gcb-pubsub-subscription for GCB... 
Created subscription [projects/biometric-dev/subscriptions/spinnaker-1-gcb-pubsub-subscription].
.  Creating pubsub topic projects/biometric-dev/topics/spinnaker-1-notifications-topic for notifications... 
Created topic [projects/biometric-dev/topics/spinnaker-1-notifications-topic].
.  Provisioning Spinnaker resources... 
namespace/halyard created
namespace/spinnaker created
clusterrolebinding.rbac.authorization.k8s.io/spinnaker-admin created
persistentvolumeclaim/halyard-pv-claim created
statefulset.apps/spin-halyard created
service/spin-halyard created
configmap/halconfig created
job.batch/hal-deploy-apply created
Waiting on job hal-deploy-apply to complete................
.  Updating Cloud Shell landing page for unsecured Spinnaker... 
customresourcedefinition.apiextensions.k8s.io/applications.app.k8s.io created
application.app.k8s.io/spinnaker-1 created
.  Labeling resources as components of application spinnaker-1... 
service/spin-clouddriver
service/spin-deck
service/spin-echo
service/spin-front50
service/spin-gate
service/spin-igor
service/spin-kayenta
service/spin-orca
service/spin-rosco
deployment.apps/spin-clouddriver
deployment.apps/spin-deck
deployment.apps/spin-echo
deployment.apps/spin-front50
deployment.apps/spin-gate
deployment.apps/spin-igor
deployment.apps/spin-kayenta
deployment.apps/spin-orca
deployment.apps/spin-rosco
WARNING: The following filter keys were not present in any resource : entryPoint
.  Deploying audit log cloud function spinnaker1AuditLog... 
WARNING: The nodejs8 runtime is deprecated on Cloud Functions. Please migrate to a newer Node.js version (--runtime=nodejs12). See https://cloud.google.com/functions/docs/migrating/nodejs-runtimes
Deploying function (may take a while - up to 2 minutes)...working..
For Cloud Build Logs, visit: https://console.cloud.google.com/cloud-build/builds;region=us-east1/10b027af-7f30-4891-a0a4-b7457100116c?project=40440447981
Deploying function (may take a while - up to 2 minutes)...working.  

availableMemoryMb: 2048
buildId: 10b027af-7f30-4891-a0a4-b7457100116c
buildName: projects/40440447981/locations/us-east1/builds/10b027af-7f30-4891-a0a4-b7457100116c
entryPoint: spinnaker1AuditLog
httpsTrigger:
  securityLevel: SECURE_ALWAYS
  url: https://us-east1-biometric-dev.cloudfunctions.net/spinnaker1AuditLog
ingressSettings: ALLOW_ALL
labels:
  deployment-tool: cli-gcloud
name: projects/biometric-dev/locations/us-east1/functions/spinnaker1AuditLog
runtime: nodejs8
serviceAccountEmail: biometric-dev@appspot.gserviceaccount.com
sourceUploadUrl: https://storage.googleapis.com/gcf-upload-us-east1-4e7bafc9-1f96-4d46-8bfd-4368a708f8f2/8958157c-afb3-455b-a86c-5eb8960e8acb.zip
status: ACTIVE
timeout: 60s
updateTime: '2022-02-09T15:46:02.152Z'
versionId: '1'
bindings:
- members:
  - allUsers
  role: roles/cloudfunctions.invoker
etag: BwXXl7tPskc=
version: 1
/tmp/halyard.Mtd7A ~/cloudshell_open/spinnaker-for-gcp/scripts/install
.  Removing /home/michael/.hal... 
.  Copying halyard/spin-halyard-0:/home/spinnaker/.hal into /home/michael/.hal... 
tar: removing leading '/' from member names
~/cloudshell_open/spinnaker-for-gcp/scripts/install
.  Updating Cloud Shell landing page for unsecured Spinnaker... 
.  Checking for existing cluster spinnaker-1... 
/tmp/halyard.ZvARs ~/cloudshell_open/spinnaker-for-gcp/scripts/install
WARNING: The following filter keys were not present in any resource : name
.  Creating Cloud Source Repository spinnaker-1-config... 
Created [spinnaker-1-config].
WARNING: You may be billed for this repository. See https://cloud.google.com/source-repositories/docs/pricing for details.
Cloning into '/tmp/halyard.ZvARs/spinnaker-1-config'...
warning: You appear to have cloned an empty repository.
Project [biometric-dev] repository [spinnaker-1-config] was cloned to [/tmp/halyard.ZvARs/spinnaker-1-config].
.  Backing up /home/michael/.hal... 
.  Backing up Spinnaker deployment config files... 
.  Removing halyard/spin-halyard-0:/home/spinnaker/.hal... 
.  Copying /home/michael/.hal into halyard/spin-halyard-0:/home/spinnaker/.hal... 
.  Creating Kubernetes secret spinnaker-deployment containing Spinnaker deployment config files... 
secret/spinnaker-deployment created
[master (root-commit) 91b184b] Automated backup.
 13 files changed, 552 insertions(+)
 create mode 100644 .hal/config
 create mode 100644 .hal/default/profiles/clouddriver-local.yml
 create mode 100644 .hal/default/profiles/echo-local.yml
 create mode 100644 .hal/default/profiles/front50-local.yml
 create mode 100644 .hal/default/profiles/gate-local.yml
 create mode 100644 .hal/default/profiles/igor-local.yml
 create mode 100644 .hal/default/service-settings/deck.yml
 create mode 100644 .hal/default/service-settings/fiat.yml
 create mode 100644 .hal/default/service-settings/gate.yml
 create mode 100644 .hal/default/service-settings/redis.yml
 create mode 100644 deployment_config_files/config.json
 create mode 100644 deployment_config_files/index.js
 create mode 100644 deployment_config_files/properties
Enumerating objects: 20, done.
Counting objects: 100% (20/20), done.
Delta compression using up to 4 threads
Compressing objects: 100% (14/14), done.
Writing objects: 100% (20/20), 6.99 KiB | 1.75 MiB/s, done.
Total 20 (delta 0), reused 0 (delta 0)
To https://source.developers.google.com/p/biometric-dev/r/spinnaker-1-config
 * [new branch]      master -> master
~/cloudshell_open/spinnaker-for-gcp/scripts/install
Waiting on API server to come online
Waiting on storage server to come online
Waiting on orchestration engine to come online
Waiting on canary analysis engine to come online
Waiting on UI server to come online
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  9188  100  9188    0     0  70137      0 --:--:-- --:--:-- --:--:-- 70137
user
non-interactive
version
Halyard version will be 1.33.0 
Halyard will be downloaded from gs://spinnaker-artifacts/halyard 
Halyard config will come from bucket gs://halconfig 
Halconfig will be stored at /home/michael/.hal/config
Uninstall script is located at /home/michael/.hal/uninstall.sh
/home/michael/cloudshell_open/spinnaker-for-gcp/scripts/install/installhalyard.aHtd /home/michael/cloudshell_open/spinnaker-for-gcp/scripts/install
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  322M  100  322M    0     0   138M      0  0:00:02  0:00:02 --:--:--  138M
halyard/
halyard/config/
halyard/config/halyard.yml
halyard/bin/
halyard/bin/hal.bat
halyard/bin/halyard.bat
halyard/bin/hal
halyard/bin/halyard
halyard/lib/
halyard/lib/jul-to-slf4j-1.7.30.jar
halyard/lib/jmespath-java-1.11.723.jar
halyard/lib/aws-java-sdk-networkmanager-1.11.723.jar
halyard/lib/aws-java-sdk-config-1.11.723.jar
halyard/lib/netty-transport-4.1.45.Final.jar
halyard/lib/google-api-services-cloudkms-v1-rev8-1.22.0.jar
halyard/lib/maven-builder-support-3.3.9.jar
halyard/lib/aws-java-sdk-accessanalyzer-1.11.723.jar
halyard/lib/aws-java-sdk-s3-1.11.723.jar
halyard/lib/aws-java-sdk-lambda-1.11.723.jar
halyard/lib/maven-repository-metadata-3.3.9.jar
halyard/lib/aws-java-sdk-elasticache-1.11.723.jar
halyard/lib/frigga-0.23.0.jar
halyard/lib/aws-java-sdk-opsworks-1.11.723.jar
halyard/lib/client-java-api-7.0.0.jar
halyard/lib/aws-java-sdk-mechanicalturkrequester-1.11.723.jar
halyard/lib/netty-handler-4.1.45.Final.jar
halyard/lib/kotlin-stdlib-1.3.70.jar
halyard/lib/jsoup-1.8.1.jar
halyard/lib/jackson-module-jaxb-annotations-2.10.3.jar
halyard/lib/aws-java-sdk-directory-1.11.723.jar
halyard/lib/aws-java-sdk-chime-1.11.723.jar
halyard/lib/groovy-swing-2.5.9.jar
halyard/lib/aws-java-sdk-mq-1.11.723.jar
halyard/lib/awsobjectmapper-1.11.723.jar
halyard/lib/aws-java-sdk-dataexchange-1.11.723.jar
halyard/lib/aws-java-sdk-workspaces-1.11.723.jar
halyard/lib/snakeyaml-1.25.jar
halyard/lib/spring-boot-actuator-2.2.4.RELEASE.jar
halyard/lib/aws-java-sdk-servicediscovery-1.11.723.jar
halyard/lib/google-api-services-iam-v1-rev267-1.25.0.jar
halyard/lib/ant-launcher-1.9.13.jar
halyard/lib/aws-java-sdk-workdocs-1.11.723.jar
halyard/lib/aether-impl-1.1.0.jar
halyard/lib/commons-math-2.2.jar
halyard/lib/aws-java-sdk-s3control-1.11.723.jar
halyard/lib/kubernetes-client-4.6.0.jar
halyard/lib/netflix-eventbus-0.3.0.jar
halyard/lib/maven-artifact-3.3.9.jar
halyard/lib/aws-java-sdk-autoscaling-1.11.723.jar
halyard/lib/joda-convert-1.2.jar
halyard/lib/groovy-cli-commons-2.5.9.jar
halyard/lib/aws-java-sdk-migrationhub-1.11.723.jar
halyard/lib/aws-java-sdk-detective-1.11.723.jar
halyard/lib/aether-util-1.1.0.jar
halyard/lib/android-json-0.0.20131108.vaadin1.jar
halyard/lib/aws-java-sdk-iam-1.11.723.jar
halyard/lib/aws-java-sdk-codebuild-1.11.723.jar
halyard/lib/aws-java-sdk-greengrass-1.11.723.jar
halyard/lib/stringtemplate-3.2.1.jar
halyard/lib/aws-java-sdk-iotevents-1.11.723.jar
halyard/lib/opencensus-api-0.24.0.jar
halyard/lib/groovy-2.5.9.jar
halyard/lib/grpc-auth-1.8.0.jar
halyard/lib/aws-java-sdk-events-1.11.723.jar
halyard/lib/aws-java-sdk-datapipeline-1.11.723.jar
halyard/lib/aws-java-sdk-servermigration-1.11.723.jar
halyard/lib/aws-java-sdk-mobile-1.11.723.jar
halyard/lib/slf4j-api-1.7.30.jar
halyard/lib/aws-java-sdk-dynamodb-1.11.723.jar
halyard/lib/jsch.agentproxy.usocket-jna-0.0.9.jar
halyard/lib/aws-java-sdk-ec2instanceconnect-1.11.723.jar
halyard/lib/spring-webmvc-5.2.3.RELEASE.jar
halyard/lib/zjsonpatch-0.3.0.jar
halyard/lib/kork-core-7.29.4.jar
halyard/lib/nimbus-jose-jwt-6.5.1.jar
halyard/lib/jsch.agentproxy.sshagent-0.0.9.jar
halyard/lib/aws-java-sdk-qldb-1.11.723.jar
halyard/lib/compactmap-1.2.1.jar
halyard/lib/grpc-okhttp-1.8.0.jar
halyard/lib/aws-java-sdk-mediatailor-1.11.723.jar
halyard/lib/aws-java-sdk-kinesisvideosignalingchannels-1.11.723.jar
halyard/lib/tomcat-annotations-api-9.0.30.jar
halyard/lib/aws-java-sdk-codegurureviewer-1.11.723.jar
halyard/lib/org.eclipse.jgit.archive-5.4.2.201908231537-r.jar
halyard/lib/commons-compress-1.19.jar
halyard/lib/antlr-2.7.7.jar
halyard/lib/bcpkix-jdk15on-1.61.jar
halyard/lib/oci-java-sdk-core-1.5.17.jar
halyard/lib/org.osgi.core-4.3.1.jar
halyard/lib/azure-mgmt-eventhub-1.19.0.jar
halyard/lib/commons-exec-1.3.jar
halyard/lib/aws-java-sdk-machinelearning-1.11.723.jar
halyard/lib/okhttp-apache-2.7.0.jar
halyard/lib/jsch-0.1.55.jar
halyard/lib/azure-keyvault-core-0.8.0.jar
halyard/lib/aws-java-sdk-medialive-1.11.723.jar
halyard/lib/aws-java-sdk-migrationhubconfig-1.11.723.jar
halyard/lib/spring-web-5.2.3.RELEASE.jar
halyard/lib/aws-java-sdk-lexmodelbuilding-1.11.723.jar
halyard/lib/groovy-testng-2.5.9.jar
halyard/lib/netty-codec-http2-4.1.45.Final.jar
halyard/lib/aws-java-sdk-cloudhsm-1.11.723.jar
halyard/lib/aws-java-sdk-directconnect-1.11.723.jar
halyard/lib/aws-java-sdk-mediapackagevod-1.11.723.jar
halyard/lib/aws-java-sdk-mediastoredata-1.11.723.jar
halyard/lib/adapter-rxjava-2.4.0.jar
halyard/lib/aws-java-sdk-emr-1.11.723.jar
halyard/lib/aws-java-sdk-elasticsearch-1.11.723.jar
halyard/lib/groovy-console-2.5.9.jar
halyard/lib/spring-boot-properties-migrator-2.2.4.RELEASE.jar
halyard/lib/jackson-dataformat-cbor-2.10.3.jar
halyard/lib/kubernetes-model-common-4.6.0.jar
halyard/lib/front50-gcs-2.15.0.jar
halyard/lib/aws-java-sdk-waf-1.11.723.jar
halyard/lib/hk2-utils-2.6.1.jar
halyard/lib/groovy-templates-2.5.9.jar
halyard/lib/clouddriver-google-5.47.1.jar
halyard/lib/clouddriver-google-common-5.47.1.jar
halyard/lib/ivy-2.4.0.jar
halyard/lib/aws-java-sdk-fsx-1.11.723.jar
halyard/lib/aws-java-sdk-connect-1.11.723.jar
halyard/lib/aws-java-sdk-costandusagereport-1.11.723.jar
halyard/lib/bcpg-jdk15on-1.61.jar
halyard/lib/junit-4.12.jar
halyard/lib/jansi-1.11.jar
halyard/lib/aws-java-sdk-iotjobsdataplane-1.11.723.jar
halyard/lib/eureka-client-1.9.18.jar
halyard/lib/aws-java-sdk-datasync-1.11.723.jar
halyard/lib/aws-java-sdk-augmentedairuntime-1.11.723.jar
halyard/lib/aws-java-sdk-marketplacecatalog-1.11.723.jar
halyard/lib/config-1.4.0.jar
halyard/lib/cats-core-5.47.1.jar
halyard/lib/groovy-docgenerator-2.5.9.jar
halyard/lib/jackson-datatype-joda-2.10.3.jar
halyard/lib/clouddriver-cloudfoundry-5.47.1.jar
halyard/lib/commons-lang-2.6.jar
halyard/lib/resilience4j-micrometer-1.0.0.jar
halyard/lib/jakarta.inject-2.6.1.jar
halyard/lib/grpc-context-1.22.1.jar
halyard/lib/spring-context-5.2.3.RELEASE.jar
halyard/lib/jersey-entity-filtering-2.29.1.jar
halyard/lib/azure-mgmt-redis-1.19.0.jar
halyard/lib/error_prone_annotations-2.3.4.jar
halyard/lib/aws-java-sdk-resourcegroups-1.11.723.jar
halyard/lib/aws-java-sdk-pinpoint-1.11.723.jar
halyard/lib/javax.activation-api-1.2.0.jar
halyard/lib/grpc-spring-boot-starter-2.3.2.jar
halyard/lib/hibernate-validator-6.0.18.Final.jar
halyard/lib/spring-boot-starter-security-2.2.4.RELEASE.jar
halyard/lib/commons-logging-1.1.3.jar
halyard/lib/maven-aether-provider-3.3.9.jar
halyard/lib/archaius-core-0.7.7.jar
halyard/lib/client-java-7.0.0.jar
halyard/lib/aws-java-sdk-guardduty-1.11.723.jar
halyard/lib/google-api-services-appengine-v1-rev92-1.25.0.jar
halyard/lib/hamcrest-core-2.1.jar
halyard/lib/azure-mgmt-network-1.19.0.jar
halyard/lib/azure-mgmt-keyvault-1.19.0.jar
halyard/lib/kork-hystrix-7.29.4.jar
halyard/lib/azure-mgmt-locks-1.19.0.jar
halyard/lib/aws-java-sdk-groundstation-1.11.723.jar
halyard/lib/azure-keyvault-webkey-1.0.0.jar
halyard/lib/groovy-test-2.5.9.jar
halyard/lib/aws-java-sdk-athena-1.11.723.jar
halyard/lib/failsafe-1.0.4.jar
halyard/lib/hk2-locator-2.6.1.jar
halyard/lib/jline-2.14.6.jar
halyard/lib/aws-java-sdk-devicefarm-1.11.723.jar
halyard/lib/jackson-dataformat-xml-2.10.3.jar
halyard/lib/groovy-cli-picocli-2.5.9.jar
halyard/lib/org.eclipse.jgit-5.4.2.201908231537-r.jar
halyard/lib/aws-java-sdk-sqs-1.11.723.jar
halyard/lib/jakarta.ws.rs-api-2.1.6.jar
halyard/lib/azure-mgmt-msi-1.19.0.jar
halyard/lib/j2objc-annotations-1.3.jar
halyard/lib/kotlin-stdlib-common-1.3.70.jar
halyard/lib/google-http-client-jackson2-1.34.2.jar
halyard/lib/aws-java-sdk-ssooidc-1.11.723.jar
halyard/lib/aws-java-sdk-dlm-1.11.723.jar
halyard/lib/netflix-infix-0.3.0.jar
halyard/lib/bcprov-ext-jdk15on-1.61.jar
halyard/lib/jersey-hk2-2.29.1.jar
halyard/lib/aws-java-sdk-forecastquery-1.11.723.jar
halyard/lib/spring-cloud-context-2.1.2.RELEASE.jar
halyard/lib/micrometer-core-1.3.2.jar
halyard/lib/aws-java-sdk-opsworkscm-1.11.723.jar
halyard/lib/spock-spring-1.3-groovy-2.5.jar
halyard/lib/aws-java-sdk-applicationautoscaling-1.11.723.jar
halyard/lib/spring-boot-starter-web-2.2.4.RELEASE.jar
halyard/lib/aws-java-sdk-codestarconnections-1.11.723.jar
halyard/lib/aws-java-sdk-transcribe-1.11.723.jar
halyard/lib/kotlin-stdlib-jdk7-1.3.70.jar
halyard/lib/tomcat-embed-websocket-9.0.30.jar
halyard/lib/aws-java-sdk-budgets-1.11.723.jar
halyard/lib/netty-codec-http-4.1.45.Final.jar
halyard/lib/aws-java-sdk-ebs-1.11.723.jar
halyard/lib/groovy-ant-2.5.9.jar
halyard/lib/junit-platform-launcher-1.6.0.jar
halyard/lib/jsr305-3.0.2.jar
halyard/lib/azure-mgmt-sql-1.19.0.jar
halyard/lib/aws-java-sdk-cognitoidp-1.11.723.jar
halyard/lib/azure-mgmt-search-1.19.0.jar
halyard/lib/halyard-backup-1.33.0-20200325200017.jar
halyard/lib/javax.annotation-api-1.3.2.jar
halyard/lib/aws-java-sdk-mediaconnect-1.11.723.jar
halyard/lib/spring-beans-5.2.3.RELEASE.jar
halyard/lib/aws-java-sdk-glue-1.11.723.jar
halyard/lib/aws-java-sdk-cognitoidentity-1.11.723.jar
halyard/lib/antlr-runtime-3.4.jar
halyard/lib/hystrix-javanica-1.5.18.jar
halyard/lib/groovy-xml-2.5.9.jar
halyard/lib/fiat-api-1.13.1.jar
halyard/lib/spring-core-5.2.3.RELEASE.jar
halyard/lib/okhttp-urlconnection-2.7.0.jar
halyard/lib/logstash-logback-encoder-4.11.jar
halyard/lib/aws-java-sdk-appmesh-1.11.723.jar
halyard/lib/azure-mgmt-storage-1.19.0.jar
halyard/lib/automaton-1.11-8.jar
halyard/lib/clouddriver-saga-5.47.1.jar
halyard/lib/jedis-3.1.0.jar
halyard/lib/aws-java-sdk-codestarnotifications-1.11.723.jar
halyard/lib/aws-java-sdk-macie-1.11.723.jar
halyard/lib/aws-java-sdk-discovery-1.11.723.jar
halyard/lib/aws-java-sdk-sesv2-1.11.723.jar
halyard/lib/resilience4j-spring-1.0.0.jar
halyard/lib/auto-value-annotations-1.6.6.jar
halyard/lib/jackson-coreutils-1.6.jar
halyard/lib/jewelcli-0.8.9.jar
halyard/lib/junit-jupiter-api-5.6.0.jar
halyard/lib/aws-java-sdk-cognitosync-1.11.723.jar
halyard/lib/clouddriver-consul-5.47.1.jar
halyard/lib/aws-java-sdk-organizations-1.11.723.jar
halyard/lib/xpp3_min-1.1.4c.jar
halyard/lib/guava-28.2-jre.jar
halyard/lib/kotlin-reflect-1.3.70.jar
halyard/lib/grpc-protobuf-1.18.0.jar
halyard/lib/bcprov-jdk15on-1.61.jar
halyard/lib/grpc-netty-1.11.0.jar
halyard/lib/groovy-test-junit5-2.5.9.jar
halyard/lib/JavaEWAH-1.1.6.jar
halyard/lib/aws-java-sdk-globalaccelerator-1.11.723.jar
halyard/lib/opencensus-contrib-grpc-metrics-0.18.0.jar
halyard/lib/commons-codec-1.13.jar
halyard/lib/gson-fire-1.8.3.jar
halyard/lib/aws-java-sdk-robomaker-1.11.723.jar
halyard/lib/aws-java-sdk-sso-1.11.723.jar
halyard/lib/de.huxhorn.sulky.ulid-8.2.0.jar
halyard/lib/apiguardian-api-1.1.0.jar
halyard/lib/azure-client-authentication-1.6.4.jar
halyard/lib/kork-exceptions-7.29.4.jar
halyard/lib/aws-java-sdk-translate-1.11.723.jar
halyard/lib/junit-platform-engine-1.6.0.jar
halyard/lib/azure-mgmt-resources-1.19.0.jar
halyard/lib/aws-java-sdk-efs-1.11.723.jar
halyard/lib/retrofit-1.9.0.jar
halyard/lib/activation-1.1.jar
halyard/lib/junit-jupiter-engine-5.6.0.jar
halyard/lib/aspectjrt-1.9.5.jar
halyard/lib/aws-java-sdk-qldbsession-1.11.723.jar
halyard/lib/rxjava-1.3.8.jar
halyard/lib/resilience4j-ratelimiter-1.0.0.jar
halyard/lib/azure-mgmt-appservice-1.19.0.jar
halyard/lib/tomcat-embed-core-9.0.30.jar
halyard/lib/client-runtime-1.6.4.jar
halyard/lib/google-api-client-1.30.9.jar
halyard/lib/aws-java-sdk-ssm-1.11.723.jar
halyard/lib/aws-java-sdk-cloudtrail-1.11.723.jar
halyard/lib/aws-java-sdk-acmpca-1.11.723.jar
halyard/lib/aws-java-sdk-pi-1.11.723.jar
halyard/lib/spring-boot-autoconfigure-2.2.4.RELEASE.jar
halyard/lib/spring-jcl-5.2.3.RELEASE.jar
halyard/lib/google-api-services-storage-v1-rev141-1.25.0.jar
halyard/lib/aws-java-sdk-elasticloadbalancingv2-1.11.723.jar
halyard/lib/hystrix-core-1.5.18.jar
halyard/lib/aws-java-sdk-codepipeline-1.11.723.jar
halyard/lib/jsch.agentproxy.pageant-0.0.9.jar
halyard/lib/picocli-4.0.1.jar
halyard/lib/aws-java-sdk-route53resolver-1.11.723.jar
halyard/lib/spectator-ext-aws-0.103.0.jar
halyard/lib/kork-secrets-7.29.4.jar
halyard/lib/clouddriver-eureka-5.47.1.jar
halyard/lib/jersey-apache-client4-1.19.1.jar
halyard/lib/aws-java-sdk-appsync-1.11.723.jar
halyard/lib/aws-java-sdk-xray-1.11.723.jar
halyard/lib/jackson-datatype-jdk8-2.10.3.jar
halyard/lib/aws-java-sdk-eventbridge-1.11.723.jar
halyard/lib/kork-config-7.29.4.jar
halyard/lib/guice-4.1.0.jar
halyard/lib/aws-java-sdk-cloud9-1.11.723.jar
halyard/lib/aws-java-sdk-securityhub-1.11.723.jar
halyard/lib/logback-core-1.2.3.jar
halyard/lib/aws-java-sdk-outposts-1.11.723.jar
halyard/lib/resilience4j-framework-common-1.0.0.jar
halyard/lib/plexus-utils-3.0.22.jar
halyard/lib/aws-java-sdk-redshift-1.11.723.jar
halyard/lib/aws-java-sdk-rds-1.11.723.jar
halyard/lib/swagger-annotations-1.5.22.jar
halyard/lib/spring-boot-starter-json-2.2.4.RELEASE.jar
halyard/lib/aws-java-sdk-lex-1.11.723.jar
halyard/lib/aws-java-sdk-appconfig-1.11.723.jar
halyard/lib/aws-java-sdk-personalizeevents-1.11.723.jar
halyard/lib/netty-codec-socks-4.1.45.Final.jar
halyard/lib/aws-java-sdk-apigatewayv2-1.11.723.jar
halyard/lib/aws-java-sdk-mediapackage-1.11.723.jar
halyard/lib/aopalliance-repackaged-2.6.1.jar
halyard/lib/azure-mgmt-servicebus-1.19.0.jar
halyard/lib/jakarta.activation-api-1.2.1.jar
halyard/lib/aws-java-sdk-shield-1.11.723.jar
halyard/lib/dependency-management-plugin-1.0.9.RELEASE.jar
halyard/lib/opencensus-contrib-http-util-0.24.0.jar
halyard/lib/jettison-1.3.7.jar
halyard/lib/client-java-proto-7.0.0.jar
halyard/lib/clouddriver-kubernetes-v1-5.47.1.jar
halyard/lib/resilience4j-annotations-1.0.0.jar
halyard/lib/maven-model-builder-3.3.9.jar
halyard/lib/aws-java-sdk-core-1.11.723.jar
halyard/lib/kork-telemetry-7.29.4.jar
halyard/lib/azure-mgmt-containerinstance-1.19.0.jar
halyard/lib/front50-s3-2.15.0.jar
halyard/lib/tomcat-embed-el-9.0.30.jar
halyard/lib/aws-java-sdk-marketplacemeteringservice-1.11.723.jar
halyard/lib/httpclient-4.5.11.jar
halyard/lib/aws-java-sdk-route53-1.11.723.jar
halyard/lib/spring-boot-2.2.4.RELEASE.jar
halyard/lib/jackson-module-kotlin-2.10.3.jar
halyard/lib/jackson-core-2.10.3.jar
halyard/lib/spring-boot-gradle-plugin-1.4.7.RELEASE.jar
halyard/lib/kork-aws-7.29.4.jar
halyard/lib/aws-java-sdk-fms-1.11.723.jar
halyard/lib/aws-java-sdk-worklink-1.11.723.jar
halyard/lib/converter-jackson-1.9.0.jar
halyard/lib/azure-mgmt-trafficmanager-1.19.0.jar
halyard/lib/halyard-cli-1.33.0-20200325200017.jar
halyard/lib/clouddriver-aws-5.47.1.jar
halyard/lib/okhttp-2.7.0.jar
halyard/lib/clouddriver-kubernetes-5.47.1.jar
halyard/lib/aws-java-sdk-pricing-1.11.723.jar
halyard/lib/kork-security-7.29.4.jar
halyard/lib/groovy-jmx-2.5.9.jar
halyard/lib/LatencyUtils-2.0.3.jar
halyard/lib/spock-core-1.3-groovy-2.5.jar
halyard/lib/aws-java-sdk-transfer-1.11.723.jar
halyard/lib/lang-tag-1.4.4.jar
halyard/lib/validation-api-2.0.1.Final.jar
halyard/lib/commons-cli-1.4.jar
halyard/lib/builder-annotations-0.19.2.jar
halyard/lib/aws-java-sdk-docdb-1.11.723.jar
halyard/lib/aws-java-sdk-schemas-1.11.723.jar
halyard/lib/aws-java-sdk-lakeformation-1.11.723.jar
halyard/lib/aws-java-sdk-backup-1.11.723.jar
halyard/lib/fabric8-utils-2.2.216.jar
halyard/lib/azure-mgmt-batchai-1.19.0.jar
halyard/lib/aws-java-sdk-pinpointsmsvoice-1.11.723.jar
halyard/lib/aws-java-sdk-1.11.723.jar
halyard/lib/jersey-media-json-jackson-2.29.1.jar
halyard/lib/aws-java-sdk-personalize-1.11.723.jar
halyard/lib/protobuf-javanano-3.0.0-alpha-5.jar
halyard/lib/azure-mgmt-batch-1.19.0.jar
halyard/lib/okhttp-3.14.6.jar
halyard/lib/commons-collections4-4.1.jar
halyard/lib/aws-java-sdk-kinesisanalyticsv2-1.11.723.jar
halyard/lib/log4j-api-2.12.1.jar
halyard/lib/cats-redis-5.47.1.jar
halyard/lib/testng-6.13.1.jar
halyard/lib/netty-codec-4.1.45.Final.jar
halyard/lib/httpcore-4.4.13.jar
halyard/lib/junit-platform-commons-1.6.0.jar
halyard/lib/aws-java-sdk-resourcegroupstaggingapi-1.11.723.jar
halyard/lib/aws-java-sdk-stepfunctions-1.11.723.jar
halyard/lib/aws-java-sdk-iot1clickprojects-1.11.723.jar
halyard/lib/grpc-google-common-protos-1.16.0.jar
halyard/lib/aws-java-sdk-managedblockchain-1.11.723.jar
halyard/lib/resilience4j-retry-1.0.0.jar
halyard/lib/woodstox-core-6.1.1.jar
halyard/lib/kork-artifacts-7.29.4.jar
halyard/lib/aws-java-sdk-kendra-1.11.723.jar
halyard/lib/aws-java-sdk-applicationinsights-1.11.723.jar
halyard/lib/azure-1.19.0.jar
halyard/lib/aws-java-sdk-cloudfront-1.11.723.jar
halyard/lib/jcommander-1.71.jar
halyard/lib/aws-java-sdk-clouddirectory-1.11.723.jar
halyard/lib/aws-java-sdk-comprehend-1.11.723.jar
halyard/lib/aws-java-sdk-computeoptimizer-1.11.723.jar
halyard/lib/converter-jackson-2.7.1.jar
halyard/lib/aws-java-sdk-health-1.11.723.jar
halyard/lib/classmate-1.5.1.jar
halyard/lib/aws-java-sdk-quicksight-1.11.723.jar
halyard/lib/hamcrest-2.1.jar
halyard/lib/log4j-to-slf4j-2.12.1.jar
halyard/lib/ant-1.9.13.jar
halyard/lib/resilience4j-spring-boot2-1.0.0.jar
halyard/lib/ant-antlr-1.9.13.jar
halyard/lib/plexus-component-annotations-1.6.jar
halyard/lib/retrofit-2.7.1.jar
halyard/lib/guava-2.8.0.jar
halyard/lib/qdox-1.12.1.jar
halyard/lib/commons-io-2.6.jar
halyard/lib/kork-web-7.29.4.jar
halyard/lib/aws-java-sdk-elasticbeanstalk-1.11.723.jar
halyard/lib/groovy-groovydoc-2.5.9.jar
halyard/lib/aws-java-sdk-mediastore-1.11.723.jar
halyard/lib/aws-java-sdk-workmail-1.11.723.jar
halyard/lib/protobuf-java-util-3.9.1.jar
halyard/lib/aws-java-sdk-alexaforbusiness-1.11.723.jar
halyard/lib/aws-java-sdk-appstream-1.11.723.jar
halyard/lib/spring-cloud-config-server-2.1.3.RELEASE.jar
halyard/lib/joda-time-2.10.5.jar
halyard/lib/aws-java-sdk-dax-1.11.723.jar
halyard/lib/jboss-logging-3.4.1.Final.jar
halyard/lib/aws-java-sdk-connectparticipant-1.11.723.jar
halyard/lib/xstream-1.4.11.1.jar
halyard/lib/groovy-macro-2.5.9.jar
halyard/lib/aws-java-sdk-marketplaceentitlement-1.11.723.jar
halyard/lib/servo-core-0.12.21.jar
halyard/lib/kubernetes-model-4.6.0.jar
halyard/lib/google-auth-library-credentials-0.18.0.jar
halyard/lib/aws-java-sdk-textract-1.11.723.jar
halyard/lib/asm-5.0.4.jar
halyard/lib/aws-java-sdk-marketplacecommerceanalytics-1.11.723.jar
halyard/lib/kork-jedis-7.29.4.jar
halyard/lib/commons-collections-3.2.2.jar
halyard/lib/clouddriver-core-5.47.1.jar
halyard/lib/animal-sniffer-annotations-1.17.jar
halyard/lib/spring-boot-starter-tomcat-2.2.4.RELEASE.jar
halyard/lib/jsch.agentproxy.jsch-0.0.9.jar
halyard/lib/dexx-collections-0.2.jar
halyard/lib/aws-java-sdk-savingsplans-1.11.723.jar
halyard/lib/clouddriver-appengine-5.47.1.jar
halyard/lib/azure-annotations-1.8.0.jar
halyard/lib/aws-java-sdk-elastictranscoder-1.11.723.jar
halyard/lib/groovy-servlet-2.5.9.jar
halyard/lib/azure-mgmt-monitor-1.19.0.jar
halyard/lib/checker-compat-qual-2.5.2.jar
halyard/lib/stax-api-1.0.1.jar
halyard/lib/aws-java-sdk-api-gateway-1.11.723.jar
halyard/lib/aws-java-sdk-wafv2-1.11.723.jar
halyard/lib/aws-java-sdk-snowball-1.11.723.jar
halyard/lib/azure-mgmt-containerregistry-1.19.0.jar
halyard/lib/spring-boot-actuator-autoconfigure-2.2.4.RELEASE.jar
halyard/lib/aws-java-sdk-polly-1.11.723.jar
halyard/lib/azure-mgmt-cdn-1.19.0.jar
halyard/lib/jsch.agentproxy.connector-factory-0.0.9.jar
halyard/lib/aws-java-sdk-servicequotas-1.11.723.jar
halyard/lib/xmlpull-1.1.3.1.jar
halyard/lib/ant-junit-1.9.13.jar
halyard/lib/jcl-over-slf4j-1.7.30.jar
halyard/lib/spring-boot-starter-validation-2.2.4.RELEASE.jar
halyard/lib/instrumentation-api-0.4.3.jar
halyard/lib/jersey-common-2.29.1.jar
halyard/lib/spectator-ext-gc-0.103.0.jar
halyard/lib/spring-boot-starter-aop-2.2.4.RELEASE.jar
halyard/lib/stax2-api-4.2.jar
halyard/lib/google-api-services-compute-alpha-rev20200225-1.30.9.jar
halyard/lib/jakarta.annotation-api-1.3.5.jar
halyard/lib/resilience4j-circuitbreaker-1.0.0.jar
halyard/lib/azure-client-runtime-1.6.4.jar
halyard/lib/netty-resolver-4.1.45.Final.jar
halyard/lib/azure-mgmt-graph-rbac-1.19.0.jar
halyard/lib/jna-4.5.2.jar
halyard/lib/aws-java-sdk-licensemanager-1.11.723.jar
halyard/lib/annotations-3.0.0.jar
halyard/lib/halyard-web-1.33.0-20200325200017.jar
halyard/lib/javax.ws.rs-api-2.1.jar
halyard/lib/clouddriver-artifacts-5.47.1.jar
halyard/lib/google-auth-library-oauth2-http-0.18.0.jar
halyard/lib/aws-java-sdk-kinesisvideo-1.11.723.jar
halyard/lib/azure-mgmt-dns-1.19.0.jar
halyard/lib/aws-java-sdk-personalizeruntime-1.11.723.jar
halyard/lib/spring-cloud-commons-2.1.2.RELEASE.jar
halyard/lib/azure-keyvault-1.0.0.jar
halyard/lib/aws-java-sdk-dms-1.11.723.jar
halyard/lib/aws-java-sdk-imagebuilder-1.11.723.jar
halyard/lib/aws-java-sdk-cloudwatch-1.11.723.jar
halyard/lib/aws-java-sdk-kafka-1.11.723.jar
halyard/lib/grpc-core-1.18.0.jar
halyard/lib/jaxb-api-2.3.1.jar
halyard/lib/generex-1.0.2.jar
halyard/lib/protobuf-java-3.9.1.jar
halyard/lib/spectator-web-spring-0.103.0.jar
halyard/lib/azure-mgmt-cosmosdb-1.19.0.jar
halyard/lib/aws-java-sdk-acm-1.11.723.jar
halyard/lib/aws-java-sdk-comprehendmedical-1.11.723.jar
halyard/lib/netty-common-4.1.45.Final.jar
halyard/lib/aether-api-1.1.0.jar
halyard/lib/aws-java-sdk-forecast-1.11.723.jar
halyard/lib/checker-qual-2.10.0.jar
halyard/lib/commons-fileupload-1.4.jar
halyard/lib/aws-java-sdk-serverlessapplicationrepository-1.11.723.jar
halyard/lib/jackson-datatype-jsr310-2.10.3.jar
halyard/lib/moniker-0.2.0.jar
halyard/lib/aws-java-sdk-kinesis-1.11.723.jar
halyard/lib/spectator-api-0.103.0.jar
halyard/lib/HdrHistogram-2.1.11.jar
halyard/lib/aws-java-sdk-pinpointemail-1.11.723.jar
halyard/lib/okio-1.17.2.jar
halyard/lib/sundr-codegen-0.19.2.jar
halyard/lib/aopalliance-1.0.jar
halyard/lib/aws-java-sdk-mediaconvert-1.11.723.jar
halyard/lib/jinjava-2.2.3.jar
halyard/lib/aws-java-sdk-kms-1.11.723.jar
halyard/lib/spring-security-rsa-1.0.7.RELEASE.jar
halyard/lib/resilience4j-spring-boot-common-1.0.0.jar
halyard/lib/javassist-3.22.0-CR2.jar
halyard/lib/aws-java-sdk-sts-1.11.723.jar
halyard/lib/spring-cloud-config-client-2.1.3.RELEASE.jar
halyard/lib/aws-java-sdk-sagemaker-1.11.723.jar
halyard/lib/aws-java-sdk-cloudhsmv2-1.11.723.jar
halyard/lib/oci-java-sdk-common-1.5.17.jar
halyard/lib/proto-google-common-protos-1.16.0.jar
halyard/lib/kork-annotations-7.29.4.jar
halyard/lib/aws-java-sdk-iot-1.11.723.jar
halyard/lib/aws-java-sdk-elasticinference-1.11.723.jar
halyard/lib/logback-classic-1.2.3.jar
halyard/lib/accessors-smart-1.2.jar
halyard/lib/aws-java-sdk-iotthingsgraph-1.11.723.jar
halyard/lib/spring-boot-configuration-metadata-2.2.4.RELEASE.jar
halyard/lib/jakarta.xml.bind-api-2.3.2.jar
halyard/lib/adal4j-1.6.3.jar
halyard/lib/aws-java-sdk-importexport-1.11.723.jar
halyard/lib/jakarta.validation-api-2.0.2.jar
halyard/lib/osgi-resource-locator-1.0.3.jar
halyard/lib/aws-java-sdk-elasticloadbalancing-1.11.723.jar
halyard/lib/vavr-match-0.10.0.jar
halyard/lib/aws-java-sdk-codestar-1.11.723.jar
halyard/lib/spring-security-crypto-5.2.1.RELEASE.jar
halyard/lib/resilience4j-consumer-1.0.0.jar
halyard/lib/azure-mgmt-containerservice-1.19.0.jar
halyard/lib/groovy-groovysh-2.5.9.jar
halyard/lib/kork-secrets-aws-7.29.4.jar
halyard/lib/annotations-17.0.0.jar
halyard/lib/spring-boot-starter-logging-2.2.4.RELEASE.jar
halyard/lib/aws-java-sdk-ram-1.11.723.jar
halyard/lib/oauth2-oidc-sdk-5.64.4.jar
halyard/lib/jersey-client-1.19.1.jar
halyard/lib/aws-java-sdk-autoscalingplans-1.11.723.jar
halyard/lib/ion-java-1.0.2.jar
halyard/lib/maven-model-3.3.9.jar
halyard/lib/aws-java-sdk-batch-1.11.723.jar
halyard/lib/aws-java-sdk-sagemakerruntime-1.11.723.jar
halyard/lib/json-patch-1.9.jar
halyard/lib/vavr-0.10.0.jar
halyard/lib/jackson-annotations-2.10.3.jar
halyard/lib/autolink-0.10.0.jar
halyard/lib/commons-pool2-2.7.0.jar
halyard/lib/aws-java-sdk-secretsmanager-1.11.723.jar
halyard/lib/jackson-module-parameter-names-2.10.3.jar
halyard/lib/aws-java-sdk-inspector-1.11.723.jar
halyard/lib/javax.inject-1.jar
halyard/lib/commons-jxpath-1.3.jar
halyard/lib/aws-java-sdk-simpleworkflow-1.11.723.jar
halyard/lib/aws-java-sdk-codedeploy-1.11.723.jar
halyard/lib/org.eclipse.jgit.http.apache-5.1.3.201810200350-r.jar
halyard/lib/aws-java-sdk-ecs-1.11.723.jar
halyard/lib/aws-java-sdk-rekognition-1.11.723.jar
halyard/lib/aws-java-sdk-apigatewaymanagementapi-1.11.723.jar
halyard/lib/groovy-jsr223-2.5.9.jar
halyard/lib/google-oauth-client-1.30.5.jar
halyard/lib/resilience4j-core-1.0.0.jar
halyard/lib/spring-security-web-5.2.1.RELEASE.jar
halyard/lib/oci-java-sdk-workrequests-1.5.17.jar
halyard/lib/msg-simple-1.1.jar
halyard/lib/aws-java-sdk-ec2-1.11.723.jar
halyard/lib/jcip-annotations-1.0-1.jar
halyard/lib/listenablefuture-9999.0-empty-to-avoid-conflict-with-guava.jar
halyard/lib/jna-platform-4.5.2.jar
halyard/lib/resilience4j-circularbuffer-1.0.0.jar
halyard/lib/spring-security-config-5.2.1.RELEASE.jar
halyard/lib/aws-java-sdk-costexplorer-1.11.723.jar
halyard/lib/aws-java-sdk-simpledb-1.11.723.jar
halyard/lib/spring-boot-starter-actuator-2.2.4.RELEASE.jar
halyard/lib/netty-handler-proxy-4.1.45.Final.jar
halyard/lib/jersey-client-2.29.1.jar
halyard/lib/jsch.agentproxy.usocket-nc-0.0.9.jar
halyard/lib/plexus-interpolation-1.21.jar
halyard/lib/google-http-client-1.34.2.jar
halyard/lib/clouddriver-azure-5.47.1.jar
halyard/lib/resourcecify-annotations-0.19.2.jar
halyard/lib/grpc-all-1.8.0.jar
halyard/lib/aws-java-sdk-iotanalytics-1.11.723.jar
halyard/lib/front50-core-2.15.0.jar
halyard/lib/aws-java-sdk-logs-1.11.723.jar
halyard/lib/groovy-json-2.5.9.jar
halyard/lib/halyard-proto-1.33.0-20200325200017.jar
halyard/lib/aws-java-sdk-sns-1.11.723.jar
halyard/lib/aws-java-sdk-iot1clickdevices-1.11.723.jar
halyard/lib/aws-java-sdk-ioteventsdata-1.11.723.jar
halyard/lib/groovy-nio-2.5.9.jar
halyard/lib/json-smart-2.3.jar
halyard/lib/aws-java-sdk-rdsdata-1.11.723.jar
halyard/lib/netty-buffer-4.1.45.Final.jar
halyard/lib/gson-2.8.6.jar
halyard/lib/javax.mail-1.6.1.jar
halyard/lib/spring-security-core-5.2.1.RELEASE.jar
halyard/lib/aws-java-sdk-glacier-1.11.723.jar
halyard/lib/aws-java-sdk-ses-1.11.723.jar
halyard/lib/aws-java-sdk-codecommit-1.11.723.jar
halyard/lib/spring-boot-loader-tools-2.2.4.RELEASE.jar
halyard/lib/halyard-deploy-1.33.0-20200325200017.jar
halyard/lib/clouddriver-event-5.47.1.jar
halyard/lib/caffeine-2.8.0.jar
halyard/lib/clouddriver-docker-5.47.1.jar
halyard/lib/spring-boot-starter-2.2.4.RELEASE.jar
halyard/lib/spectator-ext-jvm-0.103.0.jar
halyard/lib/halyard-config-1.33.0-20200325200017.jar
halyard/lib/halyard-core-1.33.0-20200325200017.jar
halyard/lib/grpc-services-1.11.0.jar
halyard/lib/aws-java-sdk-ecr-1.11.723.jar
halyard/lib/aws-java-sdk-lightsail-1.11.723.jar
halyard/lib/grpc-protobuf-nano-1.8.0.jar
halyard/lib/aws-java-sdk-support-1.11.723.jar
halyard/lib/aws-java-sdk-iotsecuretunneling-1.11.723.jar
halyard/lib/commons-lang3-3.9.jar
halyard/lib/aws-java-sdk-models-1.11.723.jar
halyard/lib/spring-expression-5.2.3.RELEASE.jar
halyard/lib/grpc-protobuf-lite-1.18.0.jar
halyard/lib/aws-java-sdk-workmailmessageflow-1.11.723.jar
halyard/lib/azure-storage-6.1.0.jar
halyard/lib/opentest4j-1.2.0.jar
halyard/lib/jackson-dataformat-yaml-2.10.3.jar
halyard/lib/sundr-core-0.19.2.jar
halyard/lib/jsch.agentproxy.core-0.0.9.jar
halyard/lib/fiat-core-1.13.1.jar
halyard/lib/clouddriver-security-5.47.1.jar
halyard/lib/resilience4j-bulkhead-1.0.0.jar
halyard/lib/aws-java-sdk-swf-libraries-1.11.22.jar
halyard/lib/logging-interceptor-3.14.3.jar
halyard/lib/aspectjweaver-1.9.5.jar
halyard/lib/aws-java-sdk-eks-1.11.723.jar
halyard/lib/aws-java-sdk-cloudformation-1.11.723.jar
halyard/lib/aws-java-sdk-storagegateway-1.11.723.jar
halyard/lib/aether-spi-1.1.0.jar
halyard/lib/aws-java-sdk-codeguruprofiler-1.11.723.jar
halyard/lib/azure-mgmt-compute-1.19.0.jar
halyard/lib/jersey-core-1.19.1.jar
halyard/lib/spring-aop-5.2.3.RELEASE.jar
halyard/lib/sshoogr-0.9.25.jar
halyard/lib/commons-text-1.6.jar
halyard/lib/grpc-stub-1.18.0.jar
halyard/lib/aws-java-sdk-gamelift-1.11.723.jar
halyard/lib/aws-java-sdk-servicecatalog-1.11.723.jar
halyard/lib/failureaccess-1.0.1.jar
halyard/lib/aws-java-sdk-neptune-1.11.723.jar
halyard/lib/aws-java-sdk-frauddetector-1.11.723.jar
halyard/lib/aws-java-sdk-cloudsearch-1.11.723.jar
halyard/lib/groovy-datetime-2.5.9.jar
halyard/lib/jackson-databind-2.10.3.jar
halyard/lib/kork-secrets-gcp-7.29.4.jar
halyard/lib/groovy-sql-2.5.9.jar
halyard/lib/hk2-api-2.6.1.jar
halyard/lib/kotlin-stdlib-jdk8-1.3.70.jar
halyard/lib/jzlib-1.1.1.jar
halyard/lib/aws-java-sdk-amplify-1.11.723.jar
halyard/lib/btf-1.2.jar
halyard/lib/aws-java-sdk-cloudwatchmetrics-1.11.723.jar
halyard/lib/aws-java-sdk-signer-1.11.723.jar
halyard/lib/jsr311-api-1.1.1.jar
halyard/lib/commons-configuration-1.8.jar
halyard/lib/okhttp-urlconnection-3.14.2.jar
hal
update-halyard
/home/michael/cloudshell_open/spinnaker-for-gcp/scripts/install
Welcome to Cloud Shell! Type "help" to get started.
To set your Cloud Platform project in this session use “gcloud config set project [PROJECT_ID]”
The halyard daemon isn't running yet... starting it manually....
1.33.0-20200325200017

Bash auto-completion configured.
To use the auto-completion either restart your shell, or run
. /home/michael/.bashrc
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 14.3M  100 14.3M    0     0  69.5M      0 --:--:-- --:--:-- --:--:-- 69.5M
.  Checking for existing cluster spinnaker-1... 
/tmp/halyard.OfMoA ~/cloudshell_open/spinnaker-for-gcp/scripts/install
Cloning into '/tmp/halyard.OfMoA/spinnaker-1-config'...
remote: Total 20 (delta 0), reused 20 (delta 0)
Unpacking objects: 100% (20/20), done.
Project [biometric-dev] repository [spinnaker-1-config] was cloned to [/tmp/halyard.OfMoA/spinnaker-1-config].
.  Backing up /home/michael/.hal... 
.  Backing up Spinnaker deployment config files... 
.  Removing halyard/spin-halyard-0:/home/spinnaker/.hal... 
.  Copying /home/michael/.hal into halyard/spin-halyard-0:/home/spinnaker/.hal... 
.  Deleting Kubernetes secret spinnaker-deployment... 
secret "spinnaker-deployment" deleted
.  Creating Kubernetes secret spinnaker-deployment containing Spinnaker deployment config files... 
secret/spinnaker-deployment created
[master bc3d0fa] Automated backup.
 1 file changed, 2 insertions(+)
 create mode 100644 deployment_config_files/config
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 4 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 476 bytes | 476.00 KiB/s, done.
Total 4 (delta 0), reused 0 (delta 0)
To https://source.developers.google.com/p/biometric-dev/r/spinnaker-1-config
   91b184b..bc3d0fa  master -> master
~/cloudshell_open/spinnaker-for-gcp/scripts/install

.  Installation complete. 

.  Sign up for Spinnaker for GCP updates and announcements: 
.    https://groups.google.com/forum/#!forum/spinnaker-for-gcp-announce 


15 min


# Links
## Visualizations
[Google Open Source Projects - HTML5 Canvas Visualization](https://opensource.google/projects/explore/featured)

# Appendix


## Markdown
view in vcode - shift-ctrl-v
**bold**, *italic*
> blockquote
    code
1. ordered
2. lists
    1. indented
- unordered
    - list

    <code> block indented 4 spaces or in code bracket </code>

line below

---

# diagrams
https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/creating-diagrams

```mermaid
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
```


# Source Code Headers


Apache header:

    Copyright 2022 Google LLC

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        https://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
