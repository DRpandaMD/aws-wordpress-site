# aws-wordpress-site
Set up instructions and bash scripts for LAMP stack  for Wordpress on AWS

## Start Up Database

### Provision a MySQL RDS instance
- select MySQL 
- select Dev/Test
- use Multi AZ Deployment 
- select "db.t2.micro" to keep things cheap
- fill out the settings form with the DB identifier, Master Username and password
- select default VPC into the default subnet group
- make it publicly accessible 
- create a new VPC security group
- leave all other fields as default 

### Open up the MySQL port to web-dmz Security Group
- open your databse security group
- go to inbound rules and add MySQL port to your existing web-dmz (if you have one) [ it will be port 3306]


---

## Configure Web Server

- Create a Amazon AMI EC2 Instance
- use a t2.micro for lower costs
- In the configure instance details page scroll to the advanced tab 
- copy and paste the boot strap script to install Apache WordPress php and php-mysql 
- enter in the database info into WordPress
- ssh into the EC2 Server 
```
sudo su
cd /var/www/html 
nano wp-config.php
```
- copy and paste config info provide by Wordpress
- continue with installation and log in
- create Application Load Balancer
- Register the EC2 instance to the Target Group
- Update Wordpress to the DNS name of the ALB (Both wordpress address and site address)
- the page will reload and you will need to log back in.

---

### Take Snap Shot 
- go and make Image of the running instance
- give your image a name 



## Create Auto Scaling Group

### Create Lauch Configuration

- Select the AMI you created
- in Advance Details type
```
#!/bin/bash
yum update -y
```
- Create the Launch Configuration Group
- Click on Create Auto Scaling Group
- Add all Subnets
- In advance Details:
- Select the Target Group you made
- Then in Scaling Polices chose your min / max
- You can also chose the metric Default is CPU utilization 







