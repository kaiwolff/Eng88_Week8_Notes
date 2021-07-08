Day 2

Jenkins

Will be using this to automate the testing, building and publishing stages of the calculator app. When commiting without jenkisn,w e will have had to test,, and will then need ot build and ocmmit to dockerhub. JKenkins will run tests when it pickes up on a new commit, then build and push to dockerhub.

To se tup Jenkins, need to add pipleing to Jenkins.

Create a pipeline in Jenkins through new item, and then point it at the correct github repository.

Having done that, we need to start describing to Jenkins what the required steps are.

Jenkisn can be told to look for a Jenkinsfile, where the steps to take are defined.

define Pipeline, then stages. a stage is for example, cloning the git repo. This is usually followed by a build (or compile. notice that for, for example, java, compilation sould be done before the build stage and outside of Jenkins) stage where the necesary images are selected (e.g. to make sure python 3 is included), a test stage, and a deploy stage. However, it is possible to have as many stages as necessary.



Subcategory of a stage is steps. This can be separately store in a separate batch f ile for more convenient reading).

Onc ethe Jenkinsfile is pushed ot github, jenkins will read this file and run the steps described one at atime.

to push to dockerhub, need to manage credentials in jenkins dashboard

Jenkins will tag each build with a build number. this can be set to latest using the docker tag command, or by setting up the Jenkinsfile to apply the 'latest' tag to the build. The 'latest' tag will be assumed by docker to be the last stable build.

To demonstrate, have built the calculator app using jenkins, then logged into a freshly created AWS instance and run the docker container. This is convenient, but the process can be automated further. To do this, we will be moving onto Terraform:

## Terraform

Terraform offers the possibility of "infrastructure as code" by automatin the creation of cloud computing.


To get starrted with Terraform:
a) set up credentials so that infrastructure cna be started or destroyed.

main.tf file - this will hold the info

A good basic format for a main.tf file

```
terraform {
	required_providers {
		aws = {
			source = "hashicorp/aws"
			version = "~> 3.0"
			}
		}
	}

provider "aws" {
	region = "eu-west-1"
}
```

The providers and resources ahve to be defined separately

provider will need a region value assigned

resource needs a type and name, then the ami ID. Also needs instance type (eg t2.micro) whether to associate_public_ip_address, and a key name.

Once file is set up, use the command `terraform validate` to check whether the configuration is valid.

To enter plannign mode, use `terraform plan`. Will show all the properties you can choose or set.

Once plan is satisfactory, use `terraform apply` to apply. Will make you check to confirm before moving on.

To check the info of the resources created, use `terraform show`

To destroy everything that was built usign the main.tf script, use `terraform destroy`.

To configure the security group, set up a resource of type "aws_security_group"

Inbound rules are inside an ingress block, outbound by egrees. bare minimum are from_port, to_port, protocol and cidr_blocks variables.

vpc_id - need to createa  virtual provide cloud for the 