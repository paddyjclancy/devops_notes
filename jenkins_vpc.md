# VPC - Jenkins Server

###### See Jenkins VPC Diagram!!

- Jenkins server within public subnet.
- We want to push a commit into GitHub, which will trigger the Jenkins build test.


## Set up

See aws.md / vpc_aws.md for further clarity on their set up


1) AWS - Create Jenkins Security Group
	- Inbound Rules:
		- SSH (22) - My IP
		- HTTP (80 & 8080) - Anywhere
		- HTTPS (443) - Anywhere
	- Outbound default (All 0.0.0.0/0)
2) AWS - Apply SG to new J Instance
3) Provisioning, EITHER:
	- `$scp -i ~/.ssh/[KEY] environment/app/j-provision.sh ubuntu@[IPv4 Public IP]:/home/ubuntu`
	- j-provision.sh installs Java & Jenkins (See file)
4) Start Jenkins, EITHER:
	- `$sudo service jenkins start`
	- `$sudo systemctl start jenkins`
5) Navigate to [J-Server IPv4]:8080
6) Password required
	- `$sudo cat /var/lib/jenkins/secrets/initialAdminPassword`
7) Optional create admin user
8) Install Plugins
	- Suggested
	- Amazon EC2
	- NodeJS
	- Office 365
9) Create desired pipeline - SEE JENKINS101
10) Append J-SG and Public NACL inbound rules:
	- GitHub IPs (sourced:https://api.github.com/meta):		
		1) 192.30.252.0/22
    	2) 185.199.108.0/22
    	3) 140.82.112.0/20
    - Allow these into ports 22 & 9418 (Default port for Git Protocol)
11) Check webhook ping status (Github > Repo > Settings > Webhooks)