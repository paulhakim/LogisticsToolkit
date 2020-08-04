# Steps to deploy logistic toolkit infrastructure

## 1. Prereqs
    Azure Subscription
    Cloud Shell Enabled
    AZ Copy Installed: https://aka.ms/downloadazcopy-v10-windows

## Install
    Run ARM template to create storage account
    <a href="https://portal.azure.us/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fpaulhakim%2FLogisticsToolkit%2Fmaster%2FCreateStorageForImage.json"  target="_blank">
    <img src="http://azuredeploy.net/AzureGov.png"/>
    </a>
    Create a container in the storage account named images
    Explicitly add your account as Storage Blob Data Onwer
    Use AZCOPY to copy the VHD to your storage acccount:
        ```
        azcopy login --tenant-id=<AAD-TENANT-ID> --aad-endpoint "https://login.microsoftonline.us"
        ```
        azcopy copy C:\images\abcd.vhd https://storageaccountname.blob.core.usgovcloudapi.net/images --trusted-microsoft-suffixes *.core.usgovcloudapi.net
        ```
    Run ARM template to create ILT environment 
    <a href="https://portal.azure.us/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fpaulhakim%2FLogisticsToolkit%2Fmaster%2Fazuredeploy.json"  target="_blank">
    <img src="http://azuredeploy.net/AzureGov.png"/>
    </a>
    Use docker to push container image to ACR
    Use CloudShell to create and start ACI using the ACI-CmdLine.azcli file



