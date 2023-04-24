# 2 Tier app deployment

Tasks:

- [x] Copy App
- [x] Install dependencies
- [x] Ensure Security group allows port 3000
- [x] npm install from app folder location
- [x] npm start
- [x] App should be available on port 3000

# How to use SCP command to copy app folder from local-host to AWS EC2 app instance

```
scp -i "<pvt-key>" -r <copy-pathway> ubuntu@ec2-<ip-address>.eu-west-1.compute.amazonaws.com:<destination>
```
```
scp -i "tech221.pem" -r /c/Users/tahir.LAPTOP-2JTDBK37/Documents/tech_221/tech221_vagrant_vm/vagrant_file/app ubuntu@ec2-3-249-46-24.eu-west-1.compute.amazonaws.com:/home/ubuntu/     => works
```

* `scp` - copies files over ssh

* `-i "tech221.pem` - finds the private key to use

* `-r` - copies directories and all its contents

* `/c/.....(app pathway)` - path to directory to copy

* `ubuntu@ec2.....(with ip)` - uses the ssh login name and public ip of the EC2

* `:home/ubuntu` - specifies where the copied file will go on the remote server

To find pathways for files, be sure to `cd` into their location and run `pwd` to return the directory pathway.

For files use `realpath`.

Be sure to run the `scp` command into the Gitbash terminal within the `.ssh` file and not the EC2 terminal

Once it is finished copying the files over, output should be: 

![image](https://user-images.githubusercontent.com/129314018/233975963-705eb4f9-0d52-427f-8541-7cf4b9e2444b.png)


To add port 3000 we go on AWS and edit our EC2 inbound rules:

![image](https://user-images.githubusercontent.com/129314018/233978937-3bc4b243-ac38-4121-8997-fc9d246cd707.png)

# Dependencies

We run the following commands to install the dependencies:

`sudo apt-get install nodejs -y` - install nodejs

`curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash –` - update version

`sudo apt-get install nodejs -y` - install nodejs with updated version

`sudo npm install pm2 -g` - install pm2 using npm

`cd app` - navigate to folder with Node.js app

`npm install` - install dependencies needed by Node.js app

`node app.js` - Deploy app

Once deploying app, on browser type `<ip-address>:3000`, we should see:
  
![image](https://user-images.githubusercontent.com/129314018/233981897-4d246721-3d64-42f9-b986-f4382b52f29f.png)
  
  
# Create EC2 instance for database

1. On AWS, navigating to EC2 and click launch instance
2. Add your desired name and scroll to AMIs.
3.  Here we select Ubuntu 18.04, which we can find in the `Browse More AMIs`, then on `Community AMIs`, scroll or search until you see the version below.

![image](https://user-images.githubusercontent.com/129314018/234060073-1c3451f7-7fc7-4cf6-8935-66c59392d5cd.png)

4.  On Security Groups, similar to the previous one we now add SSH connections with MY IP rules, also be sure to add extra security rules for ports 27017 and 3000, for the Mongo and App respectively as shown below.

![image](https://user-images.githubusercontent.com/129314018/234060640-b0a5ca10-0194-4c35-b9cd-ac447929b2ee.png).

5. Once done `Launch Instance`, after connect to it using SSH and copying and pasting the codes as seen before in :

![image](https://user-images.githubusercontent.com/129314018/234061179-7d809120-53e1-4309-bd5e-12e448c33f87.png)

6. In this instance, this is our DB instance, we want to install MongoDB, and can be done with this series of commands

```
sudo apt update -y 

sudo apt upgrade -y

sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv D68FA50FEA312927

echo "deb https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list

sudo apt update -y 

sudo apt upgrade -y

sudo apt-get install -y mongodb-org=3.2.20 mongodb-org-server=3.2.20 mongodb-org-shell=3.2.20 mongodb-org-mongos=3.2.20 mongodb-org-tools=3.2.20

sudo systemctl start mongod
```

# Connect

1. Now we have 2 virtual machines with AWS we want to connect them
2. On the DB VM we `cd` and edit the `mongod.conf` file by using `sudo nano/etc/mongod.conf` , we change `bindIP` to 0.0.0.0
3. After saving and exiting we run `sudo systemctl restart mongod`, `sudo systemctl enable mongod` and  `sudo systemctl status mongod` to restart, enable and make sure that it is infact running
4. Moving back to our app vm we `cd` then use the command `sudo nano .bashrc`
5. This is to make our environment variable, in this case it is `DB_HOST=mongodb://<db-ip-address-ec2>:27017/posts`
6. Save and exit
7. We then do `source .bashrc` to apply the changes we made in step 5
8. `cd app` then `npm install`. Once it is done we move on to the next step
9. Enter `node seeds/seed.js` - this command is used to execute the code in the seed.js file using the Node.js runtime.
10. Enter `node app.js` - install app.js and effectively deploy the app
11. The EC2 instance IP should now be entered in the search bar like this `IP:3000/posts`

![image](https://user-images.githubusercontent.com/129314018/234063503-beb32a01-a377-4beb-adc9-8598f51032b4.png)


