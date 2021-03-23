# SSH into EC2 instance

---
author: #anzal 

---


1. Create a key pair  -> https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html#prepare-key-pair
2. Go to the folder where .pem file of key pair exists. Open a terminal here
3. Make the .pem file private 
		```chmod 400 pem_file_name.pem```
4.  Create an ec2 instance
	1.  choose the created key pair ![[Pasted image 20210323164537.png]]
5.  Run ssh
	```
	ssh -i "pem_file_name.pem" discourse@ec2-18-204-7-155.compute-1.amazonaws.com
	```
	
