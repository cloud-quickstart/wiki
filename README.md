# Wiki / Confluence site

# Google Cloud Platform

## Developer Setup
### Installing the Google Cloud SDK

https://cloud.google.com/sdk/docs/cheatsheet

#### Issue: python version error running gcloud
There are currently issues with Python 3.10+ running gcloud as of 20211121.  The temporary fix is to revert to Python 3.7 or 2.7.
After switching the following environment varable to point to an older python installation and rerunning the shell (ming64 in this case) we are good

    Before
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


### Installing the Google Cloud SDK on Windows

### Installing the Google Cloud SDK on osx

https://cloud.google.com/sdk/docs/quickstart

    biometric:google-cloud-sdk michaelobrien$ ./install.sh
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
          
      Enter a path to an rc file to update, or leave blank to use [/Users/michaelobrien/.zshrc]:  /Users/michaelobrien/.bash_profile

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
    biometric:google-cloud-sdk michaelobrien$ source ~/.bash_profile
    biometric:google-cloud-sdk michaelobrien$ gcloud version
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

* Commands that require authentication will use michael@obrienlabs.cloud by default
* Commands will reference project `biometric-334503` by default
Run `gcloud help config` to learn how to change individual settings

This gcloud configuration is called [obrienlabs-cloud]. You can create additional configurations if you work with multiple accounts and/or projects.
Run `gcloud topic configurations` to learn more.

Some things to try next:

* Run `gcloud --help` to see the Cloud Platform services you can interact with. And run `gcloud help COMMAND` to get help on any gcloud command.
* Run `gcloud topic --help` to learn about advanced features of the SDK like arg files and output formatting


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
 

    terraform destroy
    google_compute_address.ip_address: Destroying... [id=projects/dev-sphere-335220/regions/us-central1/addresses/my-address-one-doberman]
    google_compute_address.ip_address: Still destroying... [id=projects/dev-sphere-335220/regions/us-central1/addresses/my-address-one-doberman, 10s elapsed]
    google_compute_address.ip_address: Destruction complete after 11s

    random_pet.suffix: Destroying... [id=one-doberman]
    random_pet.suffix: Destruction complete after 0s
 
    Destroy complete! Resources: 2 destroyed.

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

