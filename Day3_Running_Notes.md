Terraform Continued

The VPC ID

Everythign in AWS has an Id so that we do not rely on the name. We added a block which we gave a name to , which included the subnet_id and security_group. The ID of the VPC is not static, so we would get this only once the VPC has been set up.

AWS isntance depends on all these thigns, so all the parameters have to be foudn before the creation can be handled.




When we create everything, we need to check how to check the configuration for the server. this is called "configuration-as-code"

aws_instance 


can take `self.` in similar way to how it works in OOP