# Docker - Theory
Learning Docker - https://www.docker.com/101-tutorial

PWD = Play With Docker, cloud hosted

Notes taken from PWD tutorial & Pluralsight course: Docker Deep Dive


### Architecture & Theory
Docker is modular

**Container** = An isolated area of an OS with resource usage limits applied

A container is simply another process on your machine that has been isolated from all other processes on the host machine.

That isolation leverages <ins>kernel namespaces and control groups (C groups)</ins>, features that have been in Linux for a long time. Docker has worked to make these capabilities approachable and easy to use.

When running a container, it uses an isolated filesystem. This custom filesystem is provided by a **container image**. Since the image contains the container's filesystem, it must contain everything needed to run an application - all dependencies, configuration, scripts, binaries, etc. The image also contains other configuration for the container, such as environment variables, a default command to run, and other metadata.

A **Dockerfile** is simply a text-based script of instructions that is used to create a container image:

```
FROM node:10-alpine					  # This image is not stored locally, so will be fetched
WORKDIR /app
COPY . .
RUN yarn install --production			# yarn is an alternative to npm
CMD ["node", "/app/src/index.js"]		# Specifies default command to run when starting container from image
```

##### Kernel Internals
A container uses two main building blocks - **namespaces** and **control groups**.

Namespaces are about _isolation_.
- Similar to hypervisors (_Virtualbox_ etc)
- Go from one OS to multiple virtual OS, ie containers
- Containers share single kernel in host
- Generally contains:
	- Process ID _(pid)_
		- Isolates containers from one another
	- Network _(net)_
		- Gives each container its own isolated network stack
	- Filesystem / mount _(mnt)_
		- Gives each container its own root file system (C: or /)
	- Inter-process communications _(ipc)_
		- Lets containers access shared memory
	- UTS _(uts)_
		- Provides hostnames
	- User _(user)_
		- Allows differing users within containers (eg root)


Control groups (C groups) are about _setting limits_.
- Allocated amount of resources per container (CPU, disk space, RAM etc)


##### Docker Engine:
**For Linux:**

1) _Client_ asks _daemon_ for new container via _REST API_

2) _Daemon_ gets _containerd_ to start and manage containers

3) _Runc_ (at **O**pen **C**ontainer **I**nitiative layer) builds containers
- runc = Reference implementation of OCI runtime spec, default runtime of a vanilla installation of Docker


**For Windows:**

1) _Client_ asks _daemon_ for new container via _REST API_

2) Instead of containerd and runc, windows uses compute services

These low level differences do not alter user experience
