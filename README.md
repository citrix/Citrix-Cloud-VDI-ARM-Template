# Citrix Cloud Connector ARM Template

This template creates XenDesktop [Virtual Desktop Infrastructure](https://www.citrix.com/virtualization/vdi.html) (VDI) for either Client OS (Windows 10 [HUB] CBB) and Server OS (Windows Server 2016).

Virtual Desktop Infrastructure, or VDI, refers to the process of running a user desktop inside a virtual machine that lives on a server in the datacenter or Cloud. It’s a powerful form of desktop virtualization because it enables fully personalized desktops for each user with all the security and simplicity of centralized management.
VDI enables customers to streamline management and costs by consolidating and centralizing the desktops while delivering end-users mobility and the freedom to access virtual desktops anytime, from anywhere, on any device.  It’s important to understand, however, that VDI is only one form of desktop virtualization.


# Pre-Requisites

* Here are the pre-requisites before you invoke the template:
* Azure VNet	: Existing Azure VNet that will be passed as Parameter, to which the CloudConnector Machine is connected.
* 2 private IP	: An unused IP for assigning to VDI Server and VDI Client
* Active Directory (AD): Join the machine to an AD domain that contains the resources and/or users for the assignment to service offerings (Active Directory schema versions 2008 R2 and later are supported).
* Existing AD Domain, DomainUserName and Domain Password used for joining Citrix Cloud Connector to AD Domain.
* Download latest RTM version of [Desktop OS Virtual Delivery Agent](https://www.citrix.com/downloads/xenapp-and-xendesktop/product-software/xenapp-and-xendesktop-714.html) for Windows 10 VDA
* Download latest RTM version of [Server OS Virtual Delivery Agent](https://www.citrix.com/downloads/xenapp-and-xendesktop/product-software/xenapp-and-xendesktop-714.html) for Windows Server VDA
* Upload it to a share that can be accessed by Azure Resource Manager Template.


# Click the button below to deploy

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fcitrix%2FCitrixCloudConnector-Deployment-Arm-Templates%2Fmaster%2FmainTemplate.json" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png"/>
</a>


# Template parameters:

(Please refer to parameters.json to see sample parameter.)

| Name   | Description    |
|:--- |:---|
| vhdStorageType | Specifies the type of storage account, if being created. | 
| vhdStorageNewOrExisting | Specifies whether the storage account should be created or already exists. | 
| userImageContainerName | Specifies a storage container in the account specified by 'vhdStorageAccount' in which user images of XenApp 7.7 reside. | 
| machineSize | Specifies the size of the virtual machines (6). | 
| adminUsername | Specifies the name of the administrator for machines, Active Directory domain, NetScaler and XenApp. Exclusion list: 'admin','administrator'. Must be no more than 9 alphanumeric characters. | 
| adminPassword	| Specifies the password of the administrator for machines, Active Directory domain, NetScaler and XenApp. | 
| vnetName	|	VirtualNetwork Name in which the CloudConnector will be Installed.	|
| domainName | Specifies the name of the newly created Active Directory domain. | 
| domainUsername | Specifies the name Existing domain Username that will be used to Join Domain. | 
| domainPassword | Specifies the Existing domain Password for Domain User that will be used to Join Domain. | 
| domainControllerIp |	Private IP of Domain Controller, This is used to Join and Register CloudConnector to DomainController. |
| artifactsBaseUrl	| Specifies the base location of the child templates and desired state configuration scripts. |
| artifactsBaseUrlSasToken	|	Specifies the shared access signature token which provides access to the base artifacts location. |
| azureGov	| Specifies the shared access signature token which provides access to the base artifacts location. |
| cloudConnectorFQDN	| Specify FQDN of CloudConnector VM for Example: cloudconnectorvm.domain.com. |

| createMasterImage | Specify if you want the VDI to be created as master Image, Note: If this option is specified the VDI are not provisioned to DDC. | 
| createClientVDI | Creates a Windows 10 [HUB] CBB Image, if your subscription is not part of Azure Enterprise Agreement, choose "false", the ARM Template will not create Windows 10 [HUB] CBB VM. | 
| clientVDIPrivateIp |	Specifies an Unused Private IP Address to assign to VDI Client VM. |
| ClientVDIInstallerUri	| Url for the Standalone Desktop OS Virtual Delivery Agent Installer, which can be download [here](https://www.citrix.com/downloads/xenapp-and-xendesktop/product-software/xenapp-and-xendesktop-714.html). |
| createServerVDI	|	Specifies the shared access signature token which provides access to the base artifacts location. |
| serverVDIPrivateIp	| Specifies an Unused Private IP Address to assign to VDI Server VM. |
| serverVDIInstallerUri	| The Standalone Server OS Virtual Delivery Agent Installer, which can be downloaded [here](https://www.citrix.com/downloads/xenapp-and-xendesktop/product-software/xenapp-and-xendesktop-714.html). |
