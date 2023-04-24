# 2 Tier app deployment
# How to use SCP command to copy app folder from local-host to AWS EC2 app instance

```
scp -i "<pvt-key>" -r <copy-pathway> ubuntu@ec2-<ip-address>.eu-west-1.compute.amazonaws.com:<destination>
```
```
scp -i "tech221.pem" -r /c/Users/tahir.LAPTOP-2JTDBK37/Documents/tech_221/tech221_vagrant_vm/vagrant_file/app ubuntu@ec2-3-249-46-24.eu-west-1.compute.amazonaws.com:/home/ubuntu/     => works
```


`scp` - copies files over ssh
`-i "tech221.pem` - finds the private key to use
`-r` - copies directories and all its contents
`/c/.....(app pathway)` - path to directory to copy
`ubuntu@ec2.....(with ip)` - uses the ssh login name and public ip of the EC2
`:home/ubuntu` - specifies where the copied file will go on the remote server

