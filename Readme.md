# Steps to deploy logistic toolkit infrastructure

## Prereqs
    Azure Subscription
    Cloud Shell Enabled
    AZ Copy Installed: https://aka.ms/downloadazcopy-v10-windows

Install
    1. Run ARM template to create storage account
    <a href="https://portal.azure.us/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fpaulhakim%2FLogisticsToolkit%2Fmaster%2FCreateStorageForImage.json"  target="_blank">
    <img src="http://azuredeploy.net/AzureGov.png"/>
    </a>
    2. Create a container in the storage account named images
    3. Explicitly add your account as Storage Blob Data Onwer
    4. Use AZCOPY to copy the VHD to your storage acccount:
        ```
        azcopy login --tenant-id=<AAD-TENANT-ID> --aad-endpoint "https://login.microsoftonline.us"
        ```
        azcopy copy C:\images\abcd.vhd https://storageaccountname.blob.core.usgovcloudapi.net/images --trusted-microsoft-suffixes *.core.usgovcloudapi.net
        ```
    5. Run ARM template to create ILT environment 
    <a href="https://portal.azure.us/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fpaulhakim%2FLogisticsToolkit%2Fmaster%2Fazuredeploy.json"  target="_blank">
    <img src="http://azuredeploy.net/AzureGov.png"/>
    </a>
    6. Use docker to push container image to ACR
    7. Use CloudShell to create and start ACI using the ACI-CmdLine.azcli file



