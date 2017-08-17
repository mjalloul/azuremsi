# Deploy A Linux VM with MSI

This shows how to use Managed Service Idenity from within a Linux VM to access azure resources, in particular it shows how to:

- Create a VM with a system assigned idenity
- Install the MSI extension on the VM to allow OAuth tokens to be issued for Azure resources
- Assign RBAC permissions to the Managed Identity
- Run a script that uses azure cli 2 to login using the MSI

This template creates a new Linux VM with a MSI and deploys the MSI extension to the VM. The MSI associated with the VM is given owner permission on a storage account that is created by the template. A shell script is then run on the VM using the customscript extension , this script installs Docker and then creates a container with the Azure CLI 2, it runs a script in this container that logs in to the CLI using the token issuing endpoint installed in the VM by the MSI extension. It then uses the cli to retrieve the keys for the storage account and writes a blob with a name matching the VM name into the storage account.

The solution parameter file currently uses a preview version of the azure cli in the docker image [simongdavies/azure-cli-msi](https://hub.docker.com/r/simongdavies/azure-cli-msi/)

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fqrick26%2Fazuremsi%2Fmulti-vm%2Flinuxmsi%2Fazuredeploy.json" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png"/>
</a>
