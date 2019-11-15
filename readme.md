# Terraform

## Install terraform 
Download and install the terraform cli - https://www.terraform.io/downloads.html

## Providers
The provider block is used to configure the named provider, in this instance the Azure provider (azurerm).The Azure provider is responsible for creating and managing resources on Azure, and for all other interactions with Azure including authentication.

```terraform
# Configure the Azure Provider
provider "azurerm" {
  # whilst the 'version' attribute is optional, we recommend pinning to a given version of the Provider
  version = "~> 1.36"
}
```

## Init
The providers are made available to the Terraform as plugins. The plugin for Azure provider is "azurerm. To install azurerm provider, save the above configuration as a file with ".tf" extension, and run the below command on that directory.
```cmd
D:\Abhinab\terraform>terraform init
```
To prevent automatic upgrades to new major versions that may contain breaking changes, it is recommended to add version = "..." constraints to the corresponding provider blocks in configuration. The ~> symbol is the pessimistic constraint operator. It tells Terraform to use all non-beta versions >=1.36.0 and <1.36.0
```terraform
# Configure the Azure Provider
provider "azurerm" {
  # whilst the 'version' attribute is optional, we recommend pinning to a given version of the Provider
  version = "~> 1.36"
}
```
## Authentication
Authentication is configured in the provider block. The following example shows a configuration for authentication to Azure using service principal

```terraform
provider "azurerm" {
    version = "~>1.36"
    subscription_id = "xxxxxxxxxxxxxxxxx"
    tenant_id       = "xxxxxxxxxxxxxxxxx"
    client_secret   = "xxxxxxxxxxxxxxxxx"
    client_id       = "xxxxxxxxxxxxxxxxx"
}
```

To securely deploy Azure infrastructure, refer the following https://blog.azureandbeyond.com/2019/01/24/how-to-securely-deploy-azure-infrastructures/

## Resources
A resource block defines the desired state for a given resource within the infrastructure. The following example uses a resource block to provision a new Azure resource group. In this example, the resource type is azurerm_resource_group and the name is "rg". The resource name is used to refer to the object created in the resource block throughout the configuration. It is not the same as the name of the resource group in Azure.

```terraform
# Create a new resource group
resource "azurerm_resource_group" "rg" {
    name     = "abs-terraform-rg"
    location = "eastus"
}
```
## Plan
Create an execution plan using terraform plan. The execution plan specifies what actions Terraform will take to achieve the desired state defined in the configuration, and the order in which the actions occur. The execution plan specifies what actions Terraform will take to achieve the desired state defined in the configuration, and the order in which the actions occur.
```cmd
D:\Abhinab\terraform>terraform plan
```
Export the plan to a file using the -out argument, review the plan, and then execute that same plan. If you run terraform apply without specifying a plan, Terraform will recalculate the plan. The new plan may vary from the plan you previously created by running terraform plan.

## Apply
The terraform apply command is used to apply the changes in the configuration.
```cmd
D:\Abhinab\terraform>terraform apply
```
## Terraform State
When Terraform created the resource group it also wrote data into the terraform.tfstate file. State keeps track of the all managed resources and their associated properties with current values. Terraform state is essential for managing changes to infrastructure over time. It is necessary to preserve the state file for the entire life cycle of the resources.
```cmd
D:\Abhinab\terraform>terraform show
```
## Update exisitng infrastructure using saved Plan
As you change Terraform configurations, Terraform builds an execution plan that only modifies what is necessary to reach your desired state. Terraform builds an execution plan by comparing your desired state as described in the configuration to the current state, saved in the terraform.tfstate file or in a remote state backend. In this example, we will update tags information in the Azure Resource Group.
```terraform
resource "azurerm_resource_group" "rg" {
    name     = "abs-terraform-rg"
    location = "eastus"
    tags = {
        environment = "Abs terraform sandbox"
    }    
}
```
When a configuration is changed, the execution plan shows what actions Terraform will take to effect the change. Let's update the plan, and this time, save the plan to apply in the next step:
```cmd
# The -out argument tells Terraform to save the plan in a file named "update-rg-plan" in the current directory.
D:\Abhinab\terraform>terraform plan -out=update-rg-plan
```
This plan gets saved onto a file update-rg-plan. To make changes to the infrastructure, run the below command
```cmd
D:\Abhinab\terraform>terraform apply "update-rg-plan"
```
You can use terraform show again to see the new values associated with this resource group.

## Destroy
```cmd
# To create a plan for destroy, run the below command
D:\Abhinab\terraform>terraform plan -destroy -out=destroy-rg-plan
# To destroy, run the below command
terraform apply "destroy-rg-plan"
```