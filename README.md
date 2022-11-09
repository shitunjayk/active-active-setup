
# active-active infrastructre on azure cloud using terraform code and jenkins

## The terraform code will create the following resources
#### Resource Group
#### Virtual Network
#### Subnet
#### Public IP
#### Network Interface
#### Security Group
#### Virtual Machine


The jenkins server should have [Terraform](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli) and [Azure CLI Installed](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli) on it and logged in on to a azure account using [AZ LOGIN](https://learn.microsoft.com/en-us/cli/azure/authenticate-azure-cli)


The terraform code is divided into two directories i.e region-1 and region-2, the resources will be created in multi-region by running terraform apply in each directory at a time , which is automated with Jenkins.

![](/images/dir_structure.png)

The Jenkinsfile in this repo will create a pipeline that will create a parameterzed job that will accept apply and destroy as paramter and run the terraform code accordingly, there is approval stage before running terraform apply or destroy which will require human input then only apply/destroy stage will work, this stage is added to tackle the situation where we can accidently trigger the build even we don't want it to.
![](/images/pipeline.webp)


