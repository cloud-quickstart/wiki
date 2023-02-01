### Override Organization Policy on a Folder
vi policy.yaml

```
name: projects/690900791045/policies/gcp.resourceLocations
spec:
  rules:
    values:
      allowedValues:
       - in:canada-locations
       - in:us-locations    
```

set the orgpolicy.googleapis.com api on the project

```
gcloud org-policies set-policy policy.yaml
```
<img width="1077" alt="Screen Shot 2023-02-01 at 5 18 10 PM" src="https://user-images.githubusercontent.com/94715080/216176367-21967900-a564-4a0c-9e56-7419c5903d4e.png">

