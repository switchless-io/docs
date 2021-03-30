# Discourse


How to set up discourse with ec2 




1. Setup an ec2 instance
	1. make sure HTTPS ports are open ![[Pasted image 20210323171803.png]]
2. [[SSH into ec2 instance]]
3. Install and start docker in the machine
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
7. Start discourse setup 
	1. refer: https://github.com/discourse/discourse/blob/master/docs/INSTALL-cloud.md
	2. In case, the domain entered is not accessible by discourse server, turn off the firewall and try again![[Pasted image 20210330094212.png]]





# Appendix
Reference: https://medium.com/@axelmarcus27/how-to-configure-discourse-on-amazon-web-services-aws-e4964bcafb9


**To Re-launch discourse**

```
sudo su -
service docker start
cd /var/discourse
./discourse-setup
```

9.  In case, it throws a 'domain not accessible error', check cloudlflare settings and disable firewall and try again