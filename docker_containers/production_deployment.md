# Deployment in Production - Stacks & Services
### Big Picture
Dev View:
- An app is essentially multiple different files containing code.
- Code files _in Docker_ are then crafted into _containers_, and then multiple containers are grouped together into _services_ to create efficient scalability.
- Similar services are finally grouped together into **stacks**, this is the highest layer of the Docker operation hierarchy.

Ops View (inverse):
- Start with stack, which defines services, networks and volumes, which therefore define containers

### Stack Files
Defines a stack, a compose file, generally written in markdown (YAML).

Top level keys:
```
version:
services:
networks:
volumes:
```

Within the `services` key, there is a level-3 key - `deploy`, which allows for deployment specifications.

### Deployment & Management
When making adjustments to stack, it is best practice to edit the stack file and re-deploy, opposed to making manual adjustments in terminal / GUI.
