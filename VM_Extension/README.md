# Deploying Deep Security Agents on your Azure Virtual Machines

The repo contains in Deep_Security Install Guide Azure Marketplace

To automate the process of installing the Deep Security Agent, you can use the PowerShell script below, along with a customized JSON format
config file to install the Agent on an existing virtual machine.


## Prerequisite 
- PowerShell 3.0,  
- Azure Module 1.3.0
- Azure Management Compute 1.2.5)

### Use PowerShell Script to install Deep Security Extension on an existing virtual machine
1. Copy the text below to a text file named "private.config", and customize the content.
```
{
    "DSMname": "<DSM_Host>",
    "DSMport":"<DSM_Port>",
    "policyID":""
}
```
2. Copy the text below to a text file named `private.config` (Note : remove <DSM_tenant_id> and <DSM_tenant_password> with actual value)
```
{
    "tenantID": "<DSM_tenant_id>" ,
    "tenantPassword":"<DSM_tenant_password>"
}
```

### To add ASM VM Extension 
1. Open Azure Powershell.
2. Login in Azure Classic (ASM) by executing these command in PowerShell:
```
# Pop-up login frame and login into Azure
Add-AzureAccount
  
# List subscriptions under current login account
Get-AzureSubscription
  
# Associate subscription id with storage account
Set-AzureSubscription -SubscriptionId <change-with-subscription-id> -CurrentStorageAccount "<change-with-storage-account>"
 
# Select active subscription to be used for current session
Select-AzureSubscription -SubscriptionId <change-with-subscription-id>
```

3. Using the scripts to add ASM VM Extension as below:

Windows Virtual Machine:
```
.\DeepSecurityAddExtension_ASM_Windows_sample.ps1 -privateFileName "private.config" -publicFileName "public.config" -cloudServiceName "<cloud-service-name>" -vmName "<vm-name>"
```

Linux Virtual Machine:
```
.\DeepSecurityAddExtension_ASM_Linux_sample.ps1 -privateFileName "private.config" -publicFileName "public.config" -cloudServiceName "<cloud-service-name>" -vmName "<vm-name>"
```

### To add ARM VM Extension 
1. Open Azure Powershell.
2. Login into Azure Resource Management by executing commands in PowerShell:
```
# Pop-up login frame and login into Azure
Login-AzureRmAccount
  
# List subscriptions under current login account
Get-AzureRMSubscription
  
# List subscriptions under current login account
Get-AzureRMResourceGroup
  
# Select active subscription to be used for current session
Select-AzureRMSubscription -SubscriptionId <change-with-subscription-id>
```

Windows Virtual Machine::
```
.\DeepSecurityAddExtension_ARM_Windows_sample.ps1 -privateFileName "private.config" -publicFileName "public.config" -location "<location>" -resourceGroupName "<resource-group-name>" -vmName "<vm-name>"
```

Linux Virtual Machine::
```
.\DeepSecurityAddExtension_ARM_Linux_sample.ps1 -privateFileName "private.config" -publicFileName "public.config" -location "<location>" -resourceGroupName "<resource-group-name>" -vmName "<vm-name>"
```
