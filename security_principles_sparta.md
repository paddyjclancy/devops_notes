# Security Review before Going onto the Job :taco:

This is a collection of resources that expand on what we learned in class.
Security is a field in it's own right but as DevOps Engineers we need to security conscious and have good practices. We hold the keys to the chapel with this comes responsibility.

## Topics

### Keys and Secretes
- Areas of risk
- SSH keys
- Secrets and tokens
- .gitignore
- Environment Variable
- Hashicorp Vault https://www.vaultproject.io/

### Networking and cloud
- Networking
- IP
- Risky behaviour

### Data architecture and Data encryption
- Data
- Bastions
- Data integrity, security, high availability, Networking
- API access and N-tier
- SQL injections
- Encryption of password
- Encryption of data

### General
- Premises VS Cloud security

## **Recognising areas of risk**
The two main areas of risk you'll most likely be exposed to are:
- Dealing with Secrets and keys
- Networking of our infrastructure

### Secrets and keys
Any token that give access to code or a service **NEEDS to be taken with care.**
These include:
- SSH keys
- Authenthication tokens
- API keys
- Secretes

##### **KEY TAKEAWAY IS -> THESE NEVER EVER GO ON YOUR CODE.. you always interpolate them**

This means that you always ask two questions:
- Where do we store 'Environment variables' or these secretes and Keys?
- How do we interpolate them / use them

The two main ways of dealing with these are:
- setting Environment Variables
- using .gitignore files

#### Environment Variables
https://medium.com/chingu/an-introduction-to-environment-variables-and-how-to-use-them-f602f66d15fa

#### Managing variable on site
##### Hashicorp Vault (best)
Taking it to the next level means using a service like: Hashicorp Vault
https://www.vaultproject.io/
https://medium.com/hashicorp-engineering/essential-elements-of-vault-part-1-5a64d3de3be8
https://medium.com/hashicorp-engineering/essential-patterns-of-vault-part-2-b4d34976f1dc
https://medium.com/@maxy_ermayank/credential-store-using-hashicorp-vault-7d2fdeed08f2

##### Ansible Vault (just feature not a product like Hashicorp Vault)
https://docs.ansible.com/ansible/latest/user_guide/playbooks_vault.html

### IP and Networking Strategies
It is important to have a **clear networking strategy**.
This is mostly done by setting up the different Firewalls in AWS.

The fact that there are 3 locations can be overwhelming and confusing as well as redundant. However: **They are very important if you don't want to start mining bitcoin for someone else with your companies servers :D**

The several layers provide different levels of openness for your infrastructure.
Having different levels can also be a fail safe in case someone (or you :) ) open up a machine to the world.  

The following is the main architecture/hierarchy of the networking/Firewalls:

  world
    |
    |
   \ /
   VPC - Internet Gateway
    |
    |
   \ /
  Network table
    |
    |
   \ /
   NACLs
    |
    |
   \ /
  Subnets
    |
    |
   \ /
Security Groups  
    |
    |
   \ /
EC2 instance

##### Read here for Strategies
https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/ec2-network-and-security.html

#### General strategies

##### VPC - Gateway

##### Networking tables

##### Subnets

##### NACLs

##### Security Groups

##### Instance (internal)

##### Also N-tier, bastions and API


### Other areas to research
- Locking your computer
- password management
  - lastpass https://www.lastpass.com/solutions/business-password-manager
- Active monitoring
  - CPU usage
  - State changes
  - Data transfer
  - monitoring open sockets in your infrastructure
- Dodgy Activities
- Dodgy IPs (tor network)
- Routing, Virtual Private Networks, and encrypted Virtual Private Networks
- Tor network
- Honey-Pots
- ddos-attack
- SQL injections
