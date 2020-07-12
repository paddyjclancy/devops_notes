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