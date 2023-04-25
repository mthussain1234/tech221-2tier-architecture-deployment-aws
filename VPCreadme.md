# VPC

## What is a VPC?

* Stands for Virtual Private Cloud
* lets you launch AWS resources in a isolated virtual network which we have defined and customized
* resembles traditional network, but you can use the scalable infrastructure of aws
* A VPC allows you to secure your virtual networking environment, including your IP addresses, subnets and network gateways.



## What are the benefits and why?
* VPC lets control of the network size, this with automation can let you scale up or down when needed
* Even if VPC is part of public cloud, as it is isolated, user data doesnt mix with the cloud providers other customers
* Easy to deploy, easy to connect to a vpc, or even on premises architecture by use of vpn
* performance is better, can allow for hybrid cloud environment, where the vpc is an extended part of their own data centre
* 


## Internet Gateway?
* VPC component allows communication between VPC and itnernet
* Enables resouces in  our public subnets (which by example is EC2 instance) to connect to internet if the resouce has a
public IP address



## What is a subnet?
* network inside a network
* make networks more efficient
* if you do subnetting, network traffic can travel shorter distances without going thru routers to reaching the destination



## What is a CIDR block?
* group of addresses with same prefix and have same number of bits
* prefix length is size of cidr block
* combining multiple cidr blocks into larger whole is supernetting
* Using CIDR we can assign an IP address to host without using standard id address classes

## Route tables
* A route table contains a set of rules, 
called routes, that determine where network traffic from your subnet or gateway is directed.
