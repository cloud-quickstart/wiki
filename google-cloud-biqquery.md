# Big Query Console/API calls

## Create Dataset
https://cloud.google.com/bigquery/docs/datasets

```
michael@cloudshell:~/bquery (biometric-ol)$ bq --location us-central1 mk --dataset biometric-ol:dataset1
Dataset 'biometric-ol:dataset1' successfully created.
```

## Create table via json schema
https://cloud.google.com/bigquery/docs/tables

```
michael@cloudshell:~/bquery (biometric-ol)$ bq mk --table biometric-ol:dataset1.table1 sample-schema.json
Table 'biometric-ol:dataset1.table1' successfully created.
```
<img width="1864" alt="Screen Shot 2023-01-24 at 21 24 27" src="https://user-images.githubusercontent.com/24765473/214466647-c90f7b4d-c197-4951-9ac4-62ef25f85087.png">

## Populate table

## Export schema from existing table

```
michael@cloudshell:~/bquery (biometric-ol)$ bq show --schema --format=prettyjson biometric-ol:dataset1.table1
[
  {
    "description": "quarter",
    "mode": "REQUIRED",
    "name": "qtr",
    "type": "STRING"
  },
  
  michael@cloudshell:~/bquery (biometric-ol)$ cat sample-schema.json
[
  {
    "name": "qtr",
    "type": "STRING",
    "mode": "REQUIRED",
    "description": "quarter"
  },
 

```
