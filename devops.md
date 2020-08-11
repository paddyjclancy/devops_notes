# DevOps?

Problem 1:
- Developers write code, in working / Dev environment
- Code works for them, passed on to Operations
- Ops cannot run app - different environments

- SOLUTION: Standardized environment <-- Virtual Machines, enter DevOps

Problem 2:
- Devlopers write code in large blocks
  - Takes time, creates large / sudden update
  - Any errors will be much harder to find

- SOLUTION: AGILE
  - Smaller, regular updates
  - Reduces feedback loop, easier to find errors (automated testing)
  - Faster updates



#### 4 Pillars of DevOps

- DevOps promotes communication and collaboration between business, development and operations --> unification
- Involves people and processes, not just tools
- Works very well with the Agile Methodology - flexibility, iteration
- DevOps is about automating the development, release and operation processes
- DevOps helps in the speed of application delivery to users
- Continous improvement, learn through feedback

1) Ease of use
  - Infrastructure needs to be easy to use for entire team

2) Flexibility
  - Allows ability to evolve

3) Robustness
  - 100% uptime
  - Fast deployment
  - Strength / Reliability of Infrastructure

4) Cost
  - Cap-ex & Op-ex
  - Cost of downtime
  - Cost of slow innovation
  - Cost of time to market
  - Cost of infrastructure

## Business scaling

###### Problem:

- Start up company, has code on one computer, using API
- Traffic is heavier than anticipated, computer struggling to handle quantity of requests.
- Upgrade in infrastructure required, fast.
- Immediate solution today --> Cloud Migration
- From there, two options

#### Vertical Scaling

- More monolithic
- Continue using one machine, however increase size / capactiy
- Pros:
  - Can be faster - Interprocess communication
  - High data consistency (availability), as all in one place
- Cons:
  - Single point of failure can bring whole system down - RISK
  - Clear hardware limitation

#### Horizontal Scaling

- The practice of using a network of machines to balance the load
- Scaling can be carried out dynamically, and without major interruption
- Pros:
  - More resilient
  - Scales very well as user traffic increases
  - No single point of failure / exposure - Risk down
- Cons:
  - Can be slower - Network Calls / Remote Procedure Call (RPCs)
  - Potential for data inconsistency due to load balancing across machines


#### Monitoring

- Example tools: AWS monitoring, ELK Stack
- Course does not cover a lot of this
- This practice provides a greater awareness of an app / product:
  - Health status
  - Robustness
  - Information of code
  - Estimate demand - plan and respond
  - Monitor security and activity



## The Future of DevOps

DevOps, which originated in the late 2000s, is by now a mature and established discipline. It’s no longer evolving as rapidly as it did in its early years. Yet there is one force that is likely to drive a new round of innovation among DevOps practitioners: The need to provide IT support and servers to remote workers.

Five likely ways DevOps may evolve in the future - Post-Covid:


###### Greater reliance on virtual collaboration tools

Organizations that in the past used tech-oriented communication tools like Slack or Trello only for technical teams may find that it makes sense to adopt them for broader groups of employees to keep communication about software delivery flowing when it’s impossible for everyone to sit down in the same room.

Technical teams that used these types of tools internally are likely to begin leaning on them more extensively as a way to interface with external teams, too.


###### Support a broader range of end user environments

When all of your users are working in the same physical office, it’s relatively easy to ensure that the hardware and software configurations on their devices do not vary too much. As a result, the number of environment variables you have to test for and address is limited.

Remote working usually implies that employees are using personal devices, which they have configured themselves. 

This is likely to drive increased use of automated testing by DevOps teams who need an efficient way of ensuring that the business apps they deploy and manage will work as required


###### Increase in cloud-based dev / test environments

Even in organizations already running production applications in the cloud, dev/test environments sometimes remain on-premises, where it is easier to redeploy code or upload data quickly.

When working remotely, these dev/test environments are more difficult to access. This may lay result in an acceleration in the use of (hybrid) cloud-based services


###### Shift to cloud-based secrets management

From a security stand point, there is the potential for an increase in the risk of security compromises due to the sharing of machines and access rights

These needs are likely to push more organizations toward a cloud-based secrets management architecture, wherein they discard on-premises password managers in favor of solutions such as AWS Secrets Manager or Azure Key Vault to secure sensitive authentication and authorization information.

This means that DevOps teams that are not yet up-to-speed with the so-called cloud-native approach to secrets management will need to get there.


###### Further agility in CI / CD

In these circumstances, software delivery teams may need to deploy new features (such as an authentication service that works with users connecting from external networks, or data-compression features that improve app performance when users are connecting from remote locations with slower Internet connections than they would have in the office) that were not part of an application’s original functionality but are crucial for supporting remote users.