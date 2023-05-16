# Google Cloud SQL
## Importing into MySQL
- add the following role = Cloud SQL Admin


## Troubleshooting
### Importing fails on SUPER role missing on identity
```
error: exit status 1 stdout(capped at 100k bytes): stderr: ERROR 1227 (42000) at line 20: Access denied; you need (at least one of) the SUPER privilege(s) for this operation
```
