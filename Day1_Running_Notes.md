Picking up where we left off on DevOps

Going to try and set up a docker container that "listens" to a github and builds a docker build automatically

Session 1

virtual Box Networking

Several scenarios

Work on adding docker container.


By default, there are four types of interface for a VM. Normally NAt is used, and everythign sent through the IP address of the host. There is one "network adapter" in the virtual machine in NAT mode. exactly the same as NAT in "real" machines. The virtual machine has an IP address, 10.0.2.15 and the same gateway. The gateway, which is VirtualBox in our case, will have a NAT Engine. The NAT is done and enables using the internet via the IP address of the physical computer. In this mode, a browser from the physical machien would be unable to access the virtual machine. The outside can only respond to requests from the internal network of VMs. This is the "most closed" mode. Each machine has its own virtual network.

Bridged Networking:

If the adapter is in bridged mode, the virtual machine will go directly to the physical machine's network, and behave as if it has a physical network adapter. The IP address is provided by the router of the physical router if it is the DHCP server. The machines can not only access each other, but every machine on the netwo-rk could interact with the virtual machine. This would allow, for example, an app or service running on a VM to be accessed by other computers on the network. This is termed an "open mode", as the virtual machien behaves as if it is a completely independent machine and connects to the network as such.

Can add up to 4 adapters to a virtual machine using VirtualBox, though the setup will need to be done while the machine is powered down.

More in-depth information on this topic: https://www.nakivo.com/blog/virtualbox-network-setting-guide/


In AWS, the virtual machine will be configurable directly with the docker container, and should (of course) be accessible from the internet.


CODEALONG

`docker run -p 5005:5000 [name of container]`

`docker build -t [repo-link e.g. kaiwolff/flask-calculator] .`

Attempting to link with github - this has become a pro feature, but will automatically build


Next Up

Can now pull images form dockerhub, which runs things locally using docker to virtualise. Can therefore automate the process. Could do this via AWS to run the calculator app. After break, will create a server to run our app.


Main Concepts of AWS

Hug amount of available infrastructure: https://aws.amazon.com/about-aws/global-infrastructure/

This makes it easy to scale, adding as many servers as needed for virtually any task. This can also be automated, adding new servers as necessary.

AMI is templated for creating new images as they are needed. (stands for Amazon machine Image)

instance - a virtual server in the cloud.

Key pair - consists of private and public key. Used to prove identity when connecting to an instance. Public Key on instnce, private key used to confirm identity.

EC2 is a virtualised server. Whenever an EC2 instance is destroyed, any data not backed up to elsewhere will be gone. To store data, can pass it to S3 (Simple Storage Service). By sending data to an S3 object, can 

S3 has 3 main components:

1. Bucket - a container of objects. Can be thought of as a drive or partition.
   
2. Objects - Objects are the fundamental entities store in S3. Consits of object data and metadata. Objects are uniquely identified by a key (name) and a version ID

3. Keys - A key is the unique identifier for an object in a bucket. Every object has exactly one key.


So, with server and storage, the next thing needed is a network. For this, we can use AWS' 

### Virtual Private Cloud (VPC)

VPC is the netoworking layer for Amazon EC2 and enables the launch of resources into a virtual network.

Key parts

VPC - virtual private cqloud - virtual network dedicated to AWS acc.

Subnet - range of IP address in the VPC

Route Table - Set of rules (aka routes) that are used to determine how network traffic is directed

VPOC endpoint - Enables private connections to your VPC to supported AWS services and a VPC endpoint

CIDR block - Classless Inter-Domain Routing. An IP address allocation and route aggregation methodology.

### Security Group

Acts as a virtual firewall to protect EC2 instances. Controls incoming and outgoing traffic.

Inbound rules control the incoming traffic to the instance, outbound rules control the outgoing traffic from instance.

AWS has a default security group if no paritcular one is selected. whenever launching a rule, this is done ocne the save or apply button is pushed. When an EC2 instance receives a package and needs to respond, it goes through all the rules.

For tutorial on starting an EC2 instance, see: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html


Once set up, and having checked security groups.


## Session 2

### Jenkins

Will be used to automate testing to deployment stage. Can run Jenkins as a container. An example of the commands needed would be:

```
git clone https://github.com/oabuoun/jenkins-blueocean-launcher.git
cd jenkins-blueocean-launcher
docker-compose up -d
```

Can set up Jenkins to look at a github repo and then get jenkins to check if the changes pass tests

You can also run jenkins on github, instead of locally.

We normally create a Jenkinsfile. In this file, we will put all the configuring tha twill be done in several stages. thus, we can automate everythign between finsihing code and uploading the docker image
