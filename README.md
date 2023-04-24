# 2 Tier app deployment

Tasks:

- [x] Copy App
- [ ] Install dependencies
- [ ] Ensure Security group allows port 3000
- [ ] npm install from app folder location
- [ ] npm start
- [ ] App should be available on port 3000

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
  
  






