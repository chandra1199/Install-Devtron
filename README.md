# Install-Devtron

# Install devtron using default values

```
helm repo add devtron https://helm.devtron.ai
helm install devtron devtron/devtron-operator --create-namespace --namespace devtroncd 
```
# Install devtron using AWS values
```
helm repo add devtron https://helm.devtron.ai
helm install devtron devtron/devtron-operator --create-namespace --namespace devtroncd \
--set configs.BLOB_STORAGE_PROVIDER=S3 \ (cm=minio)
--set configs.DEFAULT_CACHE_BUCKET=demo-s3-bucket \ (cm=devtron-ci-cache)
--set configs.DEFAULT_CACHE_BUCKET_REGION=us-east-1 \ (cm=us-east-1)
--set configs.DEFAULT_BUILD_LOGS_BUCKET=demo-s3-bucket \ (cm=devtron-ci-log)
--set configs.DEFAULT_CD_LOGS_BUCKET_REGION=us-east-1 \ (cm=us-east-1)
--set configs.ENABLE_INGRESS=true
```
Note: Note: EXTERNAL_SECRET_AMAZON_REGION cm is mandatory if u setup devtron cluster in aws 

# Install devtron using AZURE values

```
helm repo add devtron https://helm.devtron.ai
helm install devtron devtron/devtron-operator --create-namespace --namespace devtroncd \
--set secrets.AZURE_ACCOUNT_KEY=xxxxxxxxxx \  (secret="")
--set configs.BLOB_STORAGE_PROVIDER=AZURE \ (cm=minio)
--set configs.AZURE_ACCOUNT_NAME=test-account \ (cm="")
--set configs.AZURE_BLOB_CONTAINER_CI_LOG=ci-log-container \ ( cm=ci-log-container)
--set configs.AZURE_BLOB_CONTAINER_CI_CACHE=ci-cache-container (cm=ci-cache-container)
```
# Run the following command to get the default admin password. Default username is admin
```
kubectl -n devtroncd get secret devtron-secret -o jsonpath='{.data.ACD_PASSWORD}' | base64 -d
```
