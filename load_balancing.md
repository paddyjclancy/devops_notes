# Load Balancing

The process of distributing a set of tasks over a set of resources, with the aim of improving efficiency.

Can improve / optimize the response time for each task - avoids an uneven overload of node machines whilst other nodes remain unused.

Clients send requests to the load balancer, and the load balancer sends them to targets, such as EC2 instances. To configure your load balancer, you create target groups, and then register targets with your target groups. You also create listeners to check for connection requests from clients, and listener rules to route requests from clients to the targets in one or more target groups.

`ARN` = Amazon Resource Name
	- Unique identification
	- We require an ARN when you need to specify a resource unambiguously across all of AWS
	- Format:
		```
		arn:partition:service:region:account-id:resource-id
		arn:partition:service:region:account-id:resource-type/resource-id
		arn:partition:service:region:account-id:resource-type:resource-id
		```
		- Partition = group of regions
			- `aws`, `aws-cn`, `aws-us-gov`
		- Service = Identifier of AWS product
			- `s3`
		- Account-id = The ID of the AWS account that owns the resource, without the hyphens

##### Balancer

- Single point of contact for clients, before distribution to target group(s)

- Balancer sits between client devices and backend servers.
 	- https://miro.medium.com/max/625/1*S1_KaLSMqVkE-WNsBwe9pA.jpeg
	- https://docs.aws.amazon.com/elasticloadbalancing/latest/application/images/component_architecture.png

Example Terraform notation:
```
resource "aws_lb" "lbtest" {
  name               = "test" 
  internal           = false
  load_balancer_type = "network"								# Default is application
  security_groups    = ["${module.app_tier.app_sg_id}"]
}
```


##### Listener

- Checks for connection requests from clients.
- Using specified protocols / ports in the form of prioritised rules.
		- Listeners support the following protocols and ports:
			- Protocols: HTTP, HTTPS
			- Ports: 1-65535
- CONDITION --> ACTION
- There must be at least one default rule
- The rules that you define for a listener determine how the load balancer routes requests to its registered targets.
- Condition types:
	1) `host-header`
		- Route based on host name of request
	2) `http-header`
		- Route based on HTTP header of request
	3) `http-request-method`
		- Route based on HTTP request method
	4) `path-pattern`
		- Route based on path pattern in request URL
	5) `query-string`
		- Route based on key/value pairs, of value in query string
	6) `source-ip`
		- Route based on source IP address of request

- Action types:
	1) `authenticate-cognito`
		- HTTPS
		- Use Amazon Cognito to authenticate users
	2) `authenticate-oidc`
		- HTTPS
		- Use id provider that is compliant with OpenID Connect to authenticate users
	3) `fixed-response`
		- Return custom HTTP response
	4) `forward`
		- **Forward requests to specified target groups**
	5) `redirect`
		- Redirect requests from one URL to another

Example Terraform notation:
```
resource "aws_lb_listener" "front_end" {
  load_balancer_arn = "${aws_lb.lbtest.arn}"
  port              = "443"
  protocol          = "HTTPS"

  default_action {
    type             = "forward"
    target_group_arn = "${aws_lb_target_group.test.arn}"
  }
}
```


##### Target Group

- Used to route requests towards registered target(s), ie EC2 instances.
- Uses specified protocol and port number.
- Health checks can be configured and performed upon all targets specified within target group
- `ssl_policy`  determines how the system handles encrypted traffic on your network.

Example Terraform notation:
```
resource "aws_lb_target_group" "test" {
  name     = "tf-example-lb-tg"
  port     = 80
  protocol = "HTTP"
  vpc_id   = "${aws_vpc.main.id}"
}

resource "aws_vpc" "main" {
  cidr_block = "10.0.0.0/16"
}
```
