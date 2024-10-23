# ZIP Deploy a Web App to Azure App Service

## Create Azure Resources
### Login to Azure (if not already logged in)
az login

### Create resource group in Canada Central
az group create --name WebAppTest --location canadacentral

### Create App Service plan 
az appservice plan create --name flask-webapp-plan --resource-group WebAppTest --sku B1 --is-linux

### Create the web app
az webapp create --resource-group WebAppTest --plan flask-webapp-plan --name WebAppTestApp --runtime "PYTHON:3.11" --startup-file "startup.txt"

## Package and Deploy the Web App

### Zip the files
zip -r app.zip app.py requirements.txt startup.txt

### Deploy the zip
az webapp deployment source config-zip --resource-group WebAppTest --name WebAppTestApp --src app.zip