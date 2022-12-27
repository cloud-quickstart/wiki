# Project Liens - to prevent accidential deletion
## add a lien to prevent project deletion 
https://cloud.google.com/resource-manager/docs/project-liens
```
gcloud alpha resource-manager liens create --restrictions=resourcemanager.projects.delete --reason="keep project cpu/ssd quotas"
```
