# On an existing Web App, Bind a custom domain, create the DNS record to validate, Import from an App Service Certificate and Bind it

[![Deploy To Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fcoelho5br%2FDeployWebApp-ASP-Bind-Custom-Domain-and-CertificateFromAppServiceCertificate%2Fmaster%2Fazuredeploy.json)
[![Visualize](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/visualizebutton.svg?sanitize=true)](http://armviz.io/#/?load=https%3A%2F%2Fraw.githubusercontent.com%2Fcoelho5br%2FDeployWebApp-ASP-Bind-Custom-Domain-and-CertificateFromAppServiceCertificate%2Fmaster%2Fazuredeploy.json)


## To deploy this template, you need to have the following resources:

1. Domain purchased and the DNS zone that is hosted in azure. For this deployment I am considering the DNS zone is on a different resource group.
2. App Service Certificate already purchased.

It's important that the Microsoft.Azure.WebSites resource provider to have GET Access Policy right on the Key Vault, or it won't be able to import it.

On a public multi-tenanat, the Service Principal name is abfa0a7c-a6b6-4736-8310-5855508787cd .

You should run this command to give the permission:


```powershell
Connect-AzAccount
Set-AzContext -SubscriptionId SUBSCRIPTION_ID
Set-AzKeyVaultAccessPolicy -VaultName YOUR_KEYVAULT_NAME -ServicePrincipalName abfa0a7c-a6b6-4736-8310-5855508787cd -PermissionsToSecrets get
```

More information on the [Set-AzKeyVaultAccessPolicy](https://docs.microsoft.com/en-us/powershell/module/az.keyvault/set-azkeyvaultaccesspolicy?view=azps-5.5.0).

### This arm deployment will:

1. Create an App Service Plan.
2. Create an Web App.
3. Import a App Service Certificate to Web App.
4. Create a TXT and CNAME DNS record to be able to validate the Custom Domain bind.
5. Bind a Custom Domain on your app.
6. Bind the Certificate to the Custom Domain on your Web App.
