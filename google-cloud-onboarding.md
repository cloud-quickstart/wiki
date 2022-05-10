# Onboarding new Google Cloud Accounts using either gmail, workspaces or cloud identity

There are 2 primary steps when getting onboarded to cloud.  

https://cloud.google.com/billing/docs/onboarding-checklist

https://cloud.google.com/docs/enterprise/setup-checklist

# Onboarding to Google Cloud using a cloud identity account
## Google Cloud Identity

Google Cloud Identity accounts are ideal for cloud account organizations where the user identities are maintained outside of Google cloud in for example AWS Workmail or Azure Active Directory.

## Planning

Create or gain access to the domain you wish to associate or federate users from.  For example packet.global.

You will need access to the domain zone to add TXT records for domain validation under a subdomain like gcp.packet.global

Open Chrome Window with no Google Account

## Onboarding to Google Cloud using a cloud identity account and a 3rd party managed domain - AWS Route53

## Onboarding to Google Cloud using a cloud identity account and a Google managed domain
.. continuing from "open chrome window" above


Launch SignUpWithoutGmail - select gmail

https://accounts.google.com/SignUpWithoutGmail

Select gmail, register and launch a new browser - add new account - login

Create your Google Account (gmail)
<img width="1197" alt="Screen Shot 2022-05-08 at 22 10 59" src="https://user-images.githubusercontent.com/24765473/167680004-9756a577-c654-4642-9e52-d4f8e97ef2d5.png">


launch google cloud

https://console.cloud.google.com/

do not select an org yet - as the domain under GCP registration does not have an email yet and is not registered with workspace.

You will not be able to run the organization checklist account as a gmail user - https://console.cloud.google.com/cloud-setup/organization

Add Cloud Identity free in

https://cloud.google.com/identity/docs/set-up-cloud-identity-admin

follow

https://workspace.google.com/signup/gcpidentity/welcome#0

add your gmail address and GCP domain

Add email capability https://support.google.com/cloudidentity/answer/7667994

Select the email left tab on
https://domains.google.com/registrar/eventstream.dev/email?hl=en-US

Select email forwarding to to your gmail account

Launch gmail to verify email - don't worry it will launch domains in your current gmail account - verify that the verify worked in your other account that holds the domain registration

image

Check email forwarding on the DNS tab

image

wait for DNS record propagation 30 sec and recheck the cloud identity wizard warning on no email MX records

image

continue wizard regardless of warning - use your new email forward address

https://workspace.google.com/signup/gcpidentity/tos

goto setup after creation

image

Launch admin

Since I have used this phone a couple times - get past the unusual activity dialog

Identity account OK

select getting started

https://admin.google.com/u/1/ac/signup/setup/v2/gettingstarted

Verify domain - sign in option will not work on this browser - as I have it registered on another account - in this case select "Switch Verification Method" and select the 2nd TXT option.


add the TXT record

Click Verify back on the admin page

The org in this case will automatically create when you click the link below (no subdomain as the TXT record is the first on the domain.  If there is already a root domain TXT record - you will need to use a subdomain like gcp.domain.com

org is setup as the TXT record is against the root domain on the separate GCP account

# Onboarding to Google Cloud using a workspace account

## Onboarding to Google Cloud using a workspace account and a Google managed domain

# Onboarding to Google Cloud using a gmail account

https://accounts.google.com/SignUpWithoutGmail

Fill in the form with an existing email address outside of Google





Launch from step 2 of the IAM | Cloud Identity & Organization | checklist https://console.cloud.google.com/cloud-setup/organization

to https://workspace.google.com/signup/gcpidentity/welcome

# Onboarding to Google Cloud using a 3rd party email account


