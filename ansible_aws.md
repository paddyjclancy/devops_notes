# Setting up Ansible WebApp in AWS

### A) Create EC2 Instance
https://medium.com/datadriveninvestor/devops-using-ansible-to-provision-aws-ec2-instances-3d70a1cb155f

Node app should work in repo on VMs from auto provision

1) Ensure pinging is successful
2) install python-pip
	- `sudo apt install python`
	- `sudo apt-get install python-pip`
3) Install botocore
	- `pip install botocore`
4) `pip install --upgrade pip`
5) Install boto3
	- `pip install boto boto3 ansible`
6) Generate SSH keys to use for EC2 connection
	- `ssh-keygen -t rsa -b 4096 -f ~/.ssh/[pad_aws]`
7) Create directory structure:
	- `mkdir -p AWS_Ansible/group_vars/all/`
	- `cd AWS_Ansible`
	- `touch playbook.yml`
8) Create vault file for AWS key storage:
	- `ansible-vault create group_vars/all/pass.yml`
	- Enter new password for vault
9) Enter keys into file - `ec2_access_key`, `ec2_secret_key`
	- `ansible-vault edit group_vars/all/pass.yml`
10) Write playbook file (See link above)
	- Required edits:
		- id
		- region
		- image - to correspond with region
		- key_material - `~/.ssh/`
		- Uncomment `#instance_tags`, `Name:App`
			- Rename
11) To run playbook: `ansible-playbook playbook.yml --ask-vault-pass`
	- First time will gather info on AWS
12) Create instance: `ansible-playbook playbook.yml --ask-vault-pass --tags create_ec2`
13) Get public DNS: `ansible-playbook playbook.yml --ask-vault-pass`
	- Bottom line of instance output
14) SSH in from Ansible machine:
	- `ssh -i ~/.ssh/my_aws ubuntu@[DNS]`

- NB: Check new security group for HTTP / HTTPS access from local IP.

### B) Provision EC2 Instance

- In EC2 instance:
15) sshd_config file
	- `Root Permission yes`
	- `Password Login yes`
16) `sudo passwd root` --> vagrant
17) `sudo service sshd restart`
18) Test ping with `ansible all -m ping`
19) Sync app/ using play:
	- `ansible-playbook [sync_file].yml --ask-vault-pass`
17) Install nginx and set up reverse proxy using play:
	- `ansible-playbook [nginx_file].yml --ask-vault-pass`
18) Set-up and run app using play:
	- `ansible-playbook [app_play_file].yml --ask-vault-pass`
19) Go to IP address and test!



#### Learning Notes

- Copy vs Sync
	- For transferring /app, Ansible --> Instance
	- Sync MUCH faster than copy
- Try and use VIM editor over Nano	
	- More industry relevant

- Generally, naming convention is very important!!!

#### Errors Encountered

- Idempotence Error
	- Occurs when a paramater (in .yml) has been edited, but while the client token (id) remains the same	
	- Fix = Provide new id
- AWS Key issues `my_aws`
	- When creating, use proper convention