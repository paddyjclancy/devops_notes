# Terraform

- Orchestration tool used with Infrastructure as Code
- Essentially 'landscaping' infrastructure, from one machine to an entire data centre
- Generates an execution plan describing what it will do to reach desired state, before executing.

- IAC:
	- Configuration Management Tools
		- Chef, Puppet, Ansible...
		- For creating immutable infrastructure with playbooks etc...
		- If we install a package in one machine, this machine will have mutated, and change will need to be done in all others
		- End goal = AMI
	
	- Orchestration Tools
		- Terraform, Cloudform...
		- Will create infrastructure, the networking, security, monitoring and set-up around the machine that creates a production environment.
		- Eg:
			1) Automation server triggered
			2) Tests are run in machine created from AMI
			3) Test pass triggers next step on automation server
			4) New AMI created: previous AMI + changes
			5) Successful creation triggers next step in automation server
			6) Calls terraform script to create infrastructure and deploy

- The conjunction of the two allows us to define, maintain and manipulate our infrastructure as code, along with version control (git), and cloud providers (aws).

###### Terraform steps:
- Terraform creates VPC
- Creates subnets
- Adds rules and security
- Deploys AMIs and runs scripts


- Terraform will work with a cloud provider
- You will need programatic access and API keys
- Set these in environment variables (Start > Search `environment variables`), using correct naming convention
	- Can also be set within main.tf file itself (DO NOT UPLOAD TO GITHUB WITH THIS METHOD)
		- See `security.md` for more info on key security

### Terminology

- Providers
- Resources
	- ec2
- Variables

### Commands

- `terraform init`
- `terraform plan`
- `terraform apply`
- `terraform destroy`
	- Make sure to destroy once finished working!

### Modules / Separation of Concerns

In example repo - **Terraform Code-along** - the original `main.tf` file was split into sections:
	- Central
	- App (Public)
	- DB (Private)

Overall structure was as follows:

- terraform_codealong
	- modules
		- app_tier
			- main.tf
			- outputs.tf
			- variables.tf
		- db_tier
			- main.tf
			- outputs.tf
			- variables.tf
	- scripts
		- app
			- init.sh.tpl
	- main.tf
	- variables.tf


Each tier requires its own set of `main.tf` `outputs.tf` and `variables.tf`

- Relevent VPC components will be created within `main.tf`
- Individual `variables.tf` files will reference the variables used within `main.tf`
	- Point out to either external `variables.tf`, `secret_vars.tf` or `outputs.tf` of other module(s)
- Any variables that will be needed FROM a tier (in another tier) will be generated in the `outputs.tf` file
- Finally, in the primary `main.tf` file, modules will need to be referenced, as well as variables that will be used within, see example below.


### Examples

Reference to secondary module within main `main.tf`:
```
	module "app_tier" {
	  source = "./modules/app_tier" 							# locator of app main file
	  vpc_id = aws_vpc.mainvpc.id 								# reference to id of resource made in same file
	  name = var.name 											# variable created in primary variable file
	  my_ip = var.my_ip 										# variable created in primary variable file
	  internet_gateway_id = aws_internet_gateway.gw.id 		 	# reference to id of resource made in same file
	  db_private_ip = module.db_tier.db_private_ip  			# variable created in output of db_tier
	  ami_app = var.ami_app 								    # variable created in primary variable file
	}
```

Example of primary `variable.tf` file:
```	
	variable "vpc_id" {
	  type = string
	  default= "vpc-08039043ffb902e94"
	}
	
	variable "name" {
	  type = string
	  default= "Eng57.PC."
	}
```

Example of secondary `variable.tf` file (app tier):
```	
	variable "vpc_id" {
	  description = "The VPC we want the instance to launch within"  
	}
	
	variable "name" {
	  description = "Root base on naming for convention"
	}
	
	variable "my_ip" {
	  description = "Local IP to create secure port 22 connection with resources"
	}
	.....
```

Example of `outputs.tf` file (app tier):
```
	output "app_sg_id" {
	  description = "ID of app SG"
	  value = aws_security_group.sgapp.id
	}
	
	output "subpublic_cidr_block" {
	  description = "cidr_block of public subnet"
	  value = aws_subnet.subpublic.cidr_block
	}
```

