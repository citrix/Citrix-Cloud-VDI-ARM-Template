# Citrix XenApp Site Deployment Sample

This template demonstrates the creation of a self-contained XenApp environment in Azure, creating the following resources:

* Domain Controller
* XenApp Desktop Delivery Controller with SQL Express, Citrix License Server, Citrix Director, Citrix Storefront
* Citrix NetScaler
* Citrix Virtual Desktop Agents (1 RDSH & 1 Server VDI)
* RDP JumpBox

After deployment, the components are fully configured and a simple XenApp site is created in a number of steps:

1. A new user-specified Active Directory domain is created and the machines are automatically joined to it.
2. A SQL server database is configured and a site is created on the XenApp Delivery Controller.
3. VDAs are provisioned and joined to the new site.
4. A StoreFront site is created, providing access to published Apps & Desktops.
5. A certificate is obtained for the deployment from the letsencrypt certificate authority.
6. NetScaler is configured as a gateway to the deployment.

# Pre-Requisites
 
These templates make use of hidden Virtual Machine images which have the above XenApp components fully installed. 

| Image   | Description    |
|:--- |:---|
XD-ALL.vhd | XenApp 7.7 Server with StoreFront, Director, Controller & License Server.
XD-VDA.vhd | XenApp 7.7 VDA (RDS) Installation
XD-VDI.vhd | XenApp 7.7 VDA (VDI) Installation
 
Click the button below to deploy

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAsraFatima%2Fazure-quickstart-templates%2Fmaster%2Fcitrix-xd-site-basic%2FmainTemplate.json" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png"/>
</a>

Template parameters:

| Name   | Description    |
|:--- |:---|
| vhdStorageAccount | Specifies the name of the storage account used for virtual machine disks. This has to be a unique name, up to 24 chars, all lowercase. | 
| vhdStorageType | Specifies the type of storage account, if being created. | 
| vhdStorageGroup | Specifies the resource group which should contain the storage account. | 
| vhdStorageNewOrExisting | Specifies whether the storage account should be created or already exists. | 
| userImageContainerName | Specifies a storage container in the account specified by 'vhdStorageAccount' in which user images of XenApp 7.7 reside. | 
| imageType | Specifies whether the template should deploy from the Azure Marketplace gallery or from user images in the storage account specified by 'vhdStorageAccount.' | 
| imageQualifier | Specifies an additional qualifier to use for Marketplace image references. The value 'preview' is for images in staging, while the default value references production images. | 
| publicDnsName | Specifies a unique public DNS prefix for the deployment. This will produce a FQDN of the form '<publicDnsName>.<location>.cloudapp.azure.com'. Up to 62 chars, digits or dashes, lowercase, should start with a letter: must conform to '^[a-z][a-z0-9-]{1,61}[a-z0-9]. | 
| publicIpGroup | Specifies the resource group which should contain the public IP. | 
| publicIpName | Specifies the resource name for the public IP. New IPs will take this name, while references to existing ones should be valid. | 
| publicIpNewOrExisting | Specifies whether the public IP should be created or already exists. | 
| machineSize | Specifies the size of the virtual machines (6). | 
| adminUsername | Specifies the name of the administrator for machines, Active Directory domain, NetScaler and XenApp. Exclusion list: 'admin','administrator'. Must be no more than 9 alphanumeric characters. | 
| adminPassword | Specifies the password of the administrator for machines, Active Directory domain, NetScaler and XenApp. | 
| domainName | Specifies the name of the newly created Active Directory domain. | 
| siteName | Specifies the name of the XenApp site. | 
| html5Mode | Specifies whether HTML5 Reciever is to be used. | 
| emailAddress | Specifies the email address that that will be used to request a public SSL certificate for NetScaler gateway from letsencrypt.org on your behalf. This will also be used to notify you when the template has deployed successfully. | 
| acmeServer | Specifies the ACME protocol server used for public TLS certificate requests. Allowed values correspond to letsencrypt.org staging or production. | 
| customInboundRules | Specifies additional inbound NAT rules to apply in this deployment. Useful for exposing individual machines more directly. The parameter is specified as an object, as in the default. See variable 'loadBalancerSettings' for an example format. | 
| customApplications | Specifies additional applications to be installed on the VDA and published through XenApp. The parameter is specified as an array of objects, as in the default. See variables 'applications', 'vdaSettings', and 'storeFrontSettings' for an example format.  | 
| artifactsBaseUrl | Specifies the base location of the child templates and desired state configuration scripts. | 
| artifactsBaseUrlSasToken | Specifies the shared access signature token which provides access to the base artifacts location. | 

