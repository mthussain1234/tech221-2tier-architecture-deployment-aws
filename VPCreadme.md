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

## Creating a VPC

![image](https://user-images.githubusercontent.com/129314018/234364074-1983e3cc-85f0-44e2-a360-30decae93c30.png)

1. On AWS search bar type `VPC`, click and navigate to `create vpc`
2. Click and `VPC only` and change boxes as shown below (for Name tag use your own naming convention), and IPv4 CIDR is set to 10.0.0.0/16
![image](https://user-images.githubusercontent.com/129314018/234364483-3b7d2c64-1777-4d29-8e7e-4c9c43695a60.png)

## Internet Gateway (IG)

1. To create our IG we navigate to the `Create internet gateway` on the left hand side.

![image](https://user-images.githubusercontent.com/129314018/234365140-edf77741-7339-4f44-bfab-8f02da41836c.png)

2. We then name our IG, and then click `create internet gateway`
3. Once it is created we click on `actions` and then `attach to vpc`


![image](https://user-images.githubusercontent.com/129314018/234365435-fcdc234b-ae73-4a99-80f6-c2ecfb916ab9.png)

4. Choose the VPC we made before and attach them.

![image](https://user-images.githubusercontent.com/129314018/234365583-6164d23a-bf07-481f-bd9e-4fa4bb657d57.png)

## Subnets

1. Navigate to subnets, then click `create subnet`
2. On the following page click the VPC we made before and type in the CIDR block we used before

![image](https://user-images.githubusercontent.com/129314018/234366065-f7b7c83c-52a7-4891-bc40-d60892691fc2.png)

3. Then click `create subnet`

## Route table (RT)

1. Once again navigate to the `Create route tables` on left hand side, name the route table, but also signify that it is a public RT, and like before choose the VPC we made before.

![image](https://user-images.githubusercontent.com/129314018/234366308-985d8d24-fe82-4304-932f-ce11cad39c59.png)

2. On the next page, click `subnet associations` then `edit subnet associations` and add the subnet we have just made, and `save associations`.

![image](https://user-images.githubusercontent.com/129314018/234366744-01ed74b5-bd06-476b-88b0-4167e9574ce7.png)

3. Once you are back navigate to the `route` section and click `edit routes`
4. On the following page, pressing `add route` then `destination` as `0.0.0.0/0` and `target` as your internet gateway we made earlier

![image](https://user-images.githubusercontent.com/129314018/234367345-12b04bb2-a7c0-4e67-80a1-836243894ae6.png)

5. Then save changes

## NodeJs & MongoDB via VPC

1. Create AMIs for both app and db instances ( wait for statuses to be available and **initialising**)
2. Launch the EC2 instance for hte app with the AMI, but be sure to choose the subnet (public) and the VPC we made earlier (auto assign public ip is already enabled, which is fine)
3. In network settings, add SSH connection to `MY-IP`, HTTP connection to `anywhere` and a custom TCP port (3000) connection to `Anywhere` - Public
4. For private we select our VPC again, but now we select our private subnet, **be sure to disable auto assign public ip**.
5. For the ports for the private access we only add 1 which is `TCP PORT 27017` make the connection `anywhere`
6. We now ssh into our ec2 instance of app
7. Change environment variable `DB_HOST` which we access with `sudo nano .bashrc`, and the we change the IP already in there to match our private IP from the DB EC2 instance
8. We then `cd` into app folder and run `npm install`
9. We then `node seeds/seed.js` to seed the database
10. We then `npm start` in app folder to run the app
11. After entering our `public-ip>:3000/posts` - we should in fact see our Posts page working and showing data.

[ERRORS]

![image](https://user-images.githubusercontent.com/129314018/234369707-1cdb82ac-ec16-41f7-8aa8-8ec80c03b02a.png)

* I encountered this error, which clearly displays something is in fact wrong with my MongoDB server which I do not have access to
* I am still in the process of debugging this as something may have gone wrong from even before creating an AMI for the DB
* I 



  






