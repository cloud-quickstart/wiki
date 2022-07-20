# Google Cloud for AWS Developers Migration Guide


## AWS Cloud Formation to GCP Options
http://wiki.obrienlabs.cloud/display/DEV/AWS+CloudFormation

### Converting AWS Cloud Formation to GCP Terraform
I thinking a 2 step AWS cloud formation (legacy) to GCP deployment manager then GCP Deployment Manager (legacy) to Terraform
https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-guide.html
then use DM convert (I need to test this first)
https://cloud.google.com/deployment-manager/docs/dm-convert/convert

### AWS Cloud Formation capture
For autogen of Cloud Formation
In the past (pre 2017) AWS used to have a service (cloudformer) where a VM was stood up and extracted a running account into a set of cloud formation templates - I used to use this.  The side effect is the tool also generated a deployment diagram (a bit of rats nest though) that was bidirectional capable (deployment<---->diagram) mostly.   Former2 is the successor - have not tried it yet though
https://aws.amazon.com/blogs/opensource/accelerate-infrastructure-as-code-development-with-open-source-former2/

There is no direct Cloud Formation yaml to TF converter i have found yet - however I will later widen the search to CF Yaml to AWS TF provider code - as I would expect that AWS used this in the past to provision out their SEA for TF teams https://github.com/aws-samples/aws-secure-environment-accelerator
 starting with the AWS CF stack resource in TF (deploy as-is must have been the 1st step to a converter) https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudformation_stack


## Links
- GCP Crossplan Infrastructure Provider https://github.com/crossplane-contrib/provider-gcp
