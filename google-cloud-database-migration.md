# Google Cloud Database Migration
We will be migrating a single table MySQL biometric database used for heartrate/gps/sensor data with 14 million records over from AWS [RDS](https://us-east-1.console.aws.amazon.com/rds/home?region=us-east-1#databases:) to GCP [Cloud SQL](https://cloud.google.com/sql) using the GCP [Database Migration Service](https://cloud.google.com/database-migration).\
Previously we would [migrate](http://wiki.obrienlabs.cloud/display/DEV/Databases#Databases-ConnectingtoMySQL) to a local laptop first using MySQL [Workbench](https://dev.mysql.com/downloads/file/?id=514058) which results in a 6G+ SQL file with cloud egress costs of about $1.50

