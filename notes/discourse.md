# Discourse


How to set up discourse with ec2 

https://medium.com/@axelmarcus27/how-to-configure-discourse-on-amazon-web-services-aws-e4964bcafb9


1. Setup an ec2 instance
	1. make sure HTTPS ports are open ![[Pasted image 20210323171803.png]]
2. SSH into ec2 instance
3. Install docker and start
	1.  Update the packages on your instance
    
    `[ec2-user ~]$ sudo yum update -y`
    
	2.  Install Docker
    
    `[ec2-user ~]$ sudo yum install docker -y`
    
	3.  Start the Docker Service
    
    `[ec2-user ~]$ sudo service docker start`
    
	4.  Add the ec2-user to the docker group so you can execute Docker commands without using sudo.
    
    `[ec2-user ~]$ sudo usermod -a -G docker ec2-user`
4. Install git
	`sudo yum install git -y`

5. Install netcat
```
yum install nc
```
	
6. Get SMTP credentials from your email server: 
	https://github.com/discourse/discourse/blob/master/docs/INSTALL-email.md
7. Setup discourse https://github.com/discourse/discourse/blob/master/docs/INSTALL-cloud.md
	1. During the setup set the hostname as ec2's IP address: ![[Pasted image 20210323172955.png]]