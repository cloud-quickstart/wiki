# Example Terraform YaML for Google Cloud Platform
## Create a GCP Project - the simplest version
No service account impersonation yet
https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/google_project

```
vi project.tf

resource "google_project" "my_project" {
  name       = "tf-arg1"
  project_id = "tf-arg1"
  org_id     = "org-id-replace"
}

export BOOT_PROJECT_ID=pdt-arg
ORG_ID=$(gcloud projects get-ancestors $BOOT_PROJECT_ID --format='get(id)' | tail -1)
echo $ORG_ID

vi project.tf
terraform version
terraform init
terraform plan

terraform apply
  # google_project.my_project will be created
  + resource "google_project" "my_project" {
      + auto_create_network = true
      + id                  = (known after apply)
      + name                = "tf-arg1"
      + number              = (known after apply)
      + org_id              = "....."
      + project_id          = "tf-arg1"
      + skip_delete         = (known after apply)
    }

google_project.my_project: Creating...

Plan: 1 to add, 0 to change, 0 to destroy.

google_project.my_project: Creating...
google_project.my_project: Still creating... [10s elapsed]
google_project.my_project: Still creating... [20s elapsed]
google_project.my_project: Creation complete after 21s [id=projects/tf-arg1]

Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
admin_@cloudshell:~/.../tf (pdt-arg)$ gcloud config set project tf-arg1
Updated property [core/project].
```
