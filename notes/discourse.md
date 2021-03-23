# Discourse


How to set up discourse with ec2 


1. Setup an ec2 instance
	1. make sure HTTPS ports are open ![[Pasted image 20210323171803.png]]
2. SSH into ec2 instance
3. Install docker and start: https://serverfault.com/questions/836198/how-to-install-docker-on-aws-ec2-instance-with-ami-ce-ee-update
4. Install git
5. Install netcat: https://aws.amazon.com/premiumsupport/knowledge-center/cloud9-ec2-linux-2-jump-host/
	
5. Get SMTP credentials from your email server: https://github.com/discourse/discourse/blob/master/docs/INSTALL-email.md
6. Setup discourse https://github.com/discourse/discourse/blob/master/docs/INSTALL-cloud.md
	1. During the setup set the hostname as ec2's IP address: ![[Pasted image 20210323172955.png]]