# Create Ubuntu Wordpress Server for Mercury Demo at HPE Discover

### About  
This module creates a complete LAMP stack, then installs and initializes WordPress.
Once the deployment is finished, you need to go to
http://fqdn.of.your.vm/wordpress/ to finish the configuration, create an account,
and get started with WordPress.
This module uses an existing virtual network, and uses an existing network interface.  
This module also creates a public IP address for the VM.  
 

### Prerequisites  
There must be a subscription containing: a resource group, a virtual network, a network interface.  

### Parameters  
The following mandatory parameters must be provided as command line arguments to the `deploy.sh` deployment script.  
Optional parameters can also be provided for more configuration of the Wordpress server.  

declare subscriptionId=""           # MANDATORY
declare resourceGroupName=""        # MANDATORY
declare deploymentName=""           # MANDATORY
declare vmName=""                   # MANDATORY
declare adminPasswordOrKey=""       # MANDATORY
declare mySqlPassword=""            # MANDATORY
declare vmSize=""                   # MANDATORY
declare adminUsername=""            # OPTIONAL - (default: demoadmin)
declare location=""                 # OPTIONAL - (default: resourcegroup().location)
declare authenticationType=""       # OPTIONAL - (default: sshPublicKey)
**Mandatory arguments:**  

| Flag | Parameter name | Description | Type | Example value | Notes |  
|------|----------------|-------------|------|---------------|-------|  
| -a | subscriptionId | The ID of the subscription. | string | `xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx` |  |  
| -b | resourceGroupName | Is the name of an existing resource group the VM and resources will be created in. | string | `Data` |  |  
| -c | deploymentName | Is the name for this deployment. | string | `createVM` | Will be visible in the Azure Portal. |  
| -d | vmName | The name of the virtual machine that will be created. | string | `ubuntuVM` |  |  
| -e | adminPasswordOrKey | Admin password or key based on the authentication type. | secure string | `<password>` | This is a secure string and must be entered |  
| -f | mySqlPassword | mysql password. | string | `<mysql_password>` |  |  
| -g | vmSize | The size of the VM which will be created. | string | `Standard_D2s_v3` | See [Azure VM Sizes](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/sizes-general) for more VM sizes |  
|
**Optional arguments:**  

| Flag | Parameter name | Description | Type | Available options | Default value | Example value | Notes |  
|------|----------------|-------------|------|---------------|-------------------|---------------|-------|
| -h | adminUsername | The username of the admin user. | string |  | `demoadmin` | `demoadmin` |  |  
| -i | location | Location where the VM need to be created | string |  |`resourceGroup().location` | 'eastus' |  |  
| -j | authenticationType | Type of authentication to the VM. | string | `sshPublicKey` or `password` | `sshPublicKey` | `password`|  |  
  

### Usage  
Mandatory deployment script arguments:  
`-a <subscriptionId> -b <resourceGroupName> -c <deploymentName> -d <vmName> -e <adminPasswordOrKey> -f <mySqlPassword> -g <vmSize>`  

With optional arguments:  
`-a <subscriptionId> -b <resourceGroupName> -c <deploymentName> -d <vmName> -e <adminPasswordOrKey> -f <mySqlPassword> -g <vmSize> -h <adminUsername> -i <location> -j <authenticationType>`  

e.g. To run this module individually, the command below must be run from the `deploy` directory:  
`. ../modules/mercury-demo-server/deploy.sh -a <subscriptionId> -b <resourceGroupName> -c <deploymentName> -d <vmName> -e <adminPasswordOrKey> -f <mySqlPassword> -g <vmSize>`  

If mandatory parameters are not provided to the deployment script, it will check and ask for missing parameters to be entered.  
