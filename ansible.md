# Ansible and IAC

## Infrastructure as Code

- Setting up infrastructure (networks, VMs) with source code as opposed to manually.

- Source code is more robust, lack of isolation of scripts (eg provision.sh)

### Configuration Management Tools

- Tools that put IAC into practice with orchestration tools.
- Example SCM Tools:
	- Chef (ruby)
	- Puppet
	- Ansible

### Orchestration Tools

- Configure network and deployment at scale.
- Examples:
	- Ansible
	- Terraform

## Kernel

- Layer between OS and hardware
- Manages operations eg memory / CPU time

## Ansible

- A higher level language, for IAC
- Open source
- Deals with differing environments (powershell vs bash), and package managers
- Abstracts most used commands and operations in provisioning
- Allows us to become infrastructure agnostic (flexibility)
- Increases robustness due to IAS and SCM tools
- Increases ease of use (YAMLs, playbooks)
- Allows for multi and hybrid cloud-premesis-environment management (orchestration)
- Allows us to set up and track several machines such as webserver, db, AWS

### Installing

- Can't be installed straight into Windows --> use a VM

-------

1) Vagrant init
2) Vagrant file:
	- See Vagrantfile
		- Configure version (2)
		- Specify box
		- Assign IP
		- Assign hostnames

3) touch playbook.yml

```
---

- host: [APP]
  remote_user: [SUDO]
  become: true
  task:
  - name: ensure nginx is at the latest version
    apt:
      name: nginx
      state: latest
  - name: start nginx
    service: 
      name: nginx
      state: started
    become: yes
  - name: copy in app folder
    copy:
      src: ./app/
      dest: /home/ubuntu/app-from-playbook/
```

4) vagrant up

##### Inside Ansible Machine

- `$cd /etc/ansible`
- `$sudo nano hosts`:
```
	[web]
	192.168.10.10 ansible_connection=ssh ansible_ssh_user=vagrant ansible_ssh_pass=vagrant
	[db]
	192.168.10.20 ansible_connection=ssh ansible_ssh_user=vagrant ansible_ssh_pass=vagrant
	[aws]
	192.168.10.30 ansible_connection=ssh ansible_ssh_user=vagrant ansible_ssh_pass=vagrant
```
- `$ansible all -m ping`

##### Inside Agent Machines [Each Line]

- `$cd etc/ssh`
- `$sudo nano sshd_config`
	- Make `PermitRootLogin yes`
	- Make `PasswordAuthentication yes`
- `$sudo service ssh restart`
- `$sudo passwd root`
	- Enter new password: "Vagrant"

##### Back Inside Ansible Machine

- `$ssh-keygen`
- `$cd /home/vagrant/.ssh`
- `$ssh-copy-id root@[Agent IP]`
	- Enter password
- Attempt login with `ssh 'root@[Agent IP]'`
