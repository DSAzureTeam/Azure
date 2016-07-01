# Add DeepSecurity Extension (ASM/ARM) with multi-thread
## Prerequisite 
- PowerShell 3.0,  
- Azure Module 1.3.0
- Azure Management Compute 1.2.5)


### DeepSecurity VM Extension config
- Create Private configuration file and named it `private.config` and input as below. (Note : remove <DSM_tenant_id> and <DSM_tenant password> with actual value) 

`private.config`
```
{
    'tenantID': '<DSM_tenant_id>' ,
    'tenantPassword':'<DSM_tenant_password>'
}
```
Create public configuration file: `public.config`
```
{
    'DSMname': '<DSM_Host>',
    'DSMport':'<DSM_Port>',
    'policyID':''
}
```

### To add ASM VM Extension 
Login in Azure Classic (ASM) by executing these command in PowerShell:
```
# Pop-up login frame and login into Azure
Add-AzureAccount
  
# List subscriptions under current login account
Get-AzureSubscription
  
# Associate subscription id with storage account
Set-AzureSubscription -SubscriptionId <change-with-subscription-id> -CurrentStorageAccount '<change-with-storage-account>'
 
# Select active subscription to be used for current session
Select-AzureSubscription -SubscriptionId <change-with-subscription-id>
```

Using the scripts to add ASM VM Extension as below:

Windows:
```
.\DeepSecurityAddExtension_ASM_Windows_sample.ps1 -privateFileName "private.config" -publicFileName "public.config" -cloudServiceName "<cloud-service-name>" -vmName "<vm-name>"
```

Linux:
```
.\DeepSecurityAddExtension_ASM_Linux_sample.ps1 -privateFileName "private.config" -publicFileName "public.config" -cloudServiceName "<cloud-service-name>" -vmName "<vm-name>"
```

### To add ARM VM Extension 
Login into Azure Resource Management by executing commands in PowerShell:
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

Windows:
```
.\DeepSecurityAddExtension_ARM_Windows_sample.ps1 -privateFileName "private.config" -publicFileName "public.config" -location "<location>" -resourceGroupName "<resource-group-name>" -vmName "<vm-name>"
```

Linux:
```
.\DeepSecurityAddExtension_ARM_Linux_sample.ps1 -privateFileName "private.config" -publicFileName "public.config" -location "<location>" -resourceGroupName "<resource-group-name>" -vmName "<vm-name>"

```


