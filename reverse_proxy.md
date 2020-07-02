# Reverse Proxies

- Acts as a link between host client and server.
- Takes host request and passes on to other servers, delivering respective response.
- Very commonly used with nginx
- Redirecting ports

## Advantages

- Simple implementation
- Aids with load balancing and security
	- Preventing DDoS, DoS
- Low memory footprint
	- Can handle 10,000 connections from single IP

## Setup in VM - The Manual Way

https://www.hostinger.co.uk/tutorials/how-to-set-up-nginx-reverse-proxy/

1) Install nginx (May already be done)
	- `$ sudo apt-get update`
	- `$ sudo apt-get install nginx`
2) Disable default host
	- `$ sudo unlink /etc/nginx/sites-enabled/default`
3) Create proxy
	- `$ cd etc/nginx/sites-available`
	- `$ sudo nano reverse-proxy.conf`
		- Will create file
	- Use correct IP! (Vagrantfile for VM)
	- `$ server {`
    		`listen 80;`
    		`location / {`
        		`proxy_pass http://192.x.x.x:3000;`
    	    `}`
		  `}`
    - Ctrl-O, Ctrl-X
4) Link to `/sites-enabled`:
	- `$ sudo ln -s /etc/nginx/sites-available/reverse-proxy.conf /etc/nginx/sites-enabled/reverse-proxy.conf`
5) Start app
	- `$ cd /home/ubuntu/app`
	- `$ sudo service nginx restart`
	- `$ npm start`
6) Navigate to :3000 url - TEST
7) Navigate to development.local 
	- Should work