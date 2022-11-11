
# active-active infrastructre on azure cloud using terraform and jenkins

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
### For the Jenkins pipeline we willbe creating declarative pipeline with pipeline from scm. The steps are shown below for creating the jobs  for Jenkinsfile

#### 1. Ceate a pipeline job as shown in pictures below, clicking on new item and give a name and choose the type oj job
![](/images/job_creation.png)
![](/images/pipeline_job.png)

#### 2. Pipeline will be created from Jenkinsfile on our github repository, so we will choose pipeline from scm and provide the repository details.
![](/images/pipelinefromscm.png)

#### 3. Now save and click on Build Now, for the first build the job will fail because it needs to setup paramters mentioned in Jenkinsfile, for the second build it will run successfully

#### 4. Our Pipeline will look like this
![](/images/pipeline.webp)

## Author

- [@shitunjay](https://github.com/shitunjayk)
