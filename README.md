# Wiki / Confluence site

# Google Cloud Platform

## Developer Setup
### Installing the Google Cloud SDK
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
    micha@carbon MINGW64 ~
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

