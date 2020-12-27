# Getting started with Terraform Enterprise on Azure

## Create a Linux VM with infrastructure in Azure using Terraform

### Configure environment variables
Terraform Cloud creates an ephemeral VM to run Terraform operations (which create and manage your infrastructure). Set the VM's Environment Variables in the Terraform Cloud web UI to configure provider credentials.

For Azure the mandatory environment variables related to the subscription are:
1. ARM_CLIENT_ID
2. ARM_CLIENT_SECRET 
3. ARM_TENANT_ID
4. ARM_SUBSCRIPTION_ID
Optional variable is :
1. ARM_SKIP_PROVIDER_REGISTRATION

![Alt text](/images/az-env-var.jpg)

### Configurations on Azure
* Create a Resource Group in Azure with the name *rg-terraform-enterprise*
* Create a service principal and assign contributor role to the resource group

### Add code to VCS 
* Create a file called terraform_azure.tf & add the code from the file [here](/src/terraform_azure.tf)
* Add the code to VCS
* In the Terraform Enterprise UI 
    * Click the "Queue plan" menu button and provide an optional explanation. Then click the purple "Queue plan" button to start a plan.
    * Apply planned changes once the plan is complete, accept the changes by clicking the "Confirm & Apply" button

## References
* [Getting started with Terraform Enterprise](https://learn.hashicorp.com/tutorials/terraform/cloud-workspace-configure?in=terraform/cloud-get-started)
* [Create a VM in Azure with Terraform](https://docs.microsoft.com/en-us/azure/developer/terraform/create-linux-virtual-machine-with-infrastructure)
