# DNS, Route 53, Records

## DNS - Domain Name Service

- "Phone book of the internet"
- Hierarchical and decentralised naming system for computers, services and resources on either the internet or private network.
- Associates various information with domain names assigned to each of the participating entities. 

- **RECORDS:** Instructions that live in DNS servers and provide information about respective domains.
	- Contain text files written in DNS syntax



## Types of Record (Common)

- A: 
	- Holds IP address of domain
- CNAME: 
	- Forwards domain or subdomain to another
	- Does not provide IP address
- MX:
	- Directs mail to an email server
- TXT
	- Lets admin store text notes
- NS
	- Stores the name server for DNS entry
- SOA
	- Stores admin info regarding domain
- SRV
	- Specifies port for specific service
- PTR
	- Provides domain name in reverse-lookup


### A Records

- A = address
- Most fundamental type of record, indicating IP address of associated domain.
- Example: Google
	- A record will show the Google IP - 172.217.5.78

### CNAMEs

- C = canonical
- Used in lieu of A record
- When a DNS server hits records for a site, it will trigger another lookup, returning the subsequent IP

### Aliases

- Virtual record type created to provide CNAME-like behavious on domains.
- Works with Route 53
- Similar to CNAME records but resolved on server side and appear to clients as an A record
- They can be used to create transparent references to other AWS resources that only provide DNS names and not IP addresses, such as an Elastic Load Balancer or a CloudFront distribution.

### MX Records

- MX = Mail Exchange
- Indicates how email messages should be routed in accordance with standard email protocol.
- Must always point to another domain.

### TTLs

Time-to-live

- Indicates how often a DNS server will refresh a record

### Propagation

- Time frame it takes for DNS changes to be updated accross internet.
- A few hours - a few days



## Route 53

Amazon Route 53 effectively connects user requests to infrastructure running in AWS – such as Amazon EC2 instances, Elastic Load Balancing load balancers, or Amazon S3 buckets – and can also be used to route users to infrastructure outside of AWS. 

- Highly scalable and available DNS service
- Works with AWS
- Port 53s