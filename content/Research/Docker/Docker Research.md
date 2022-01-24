---
title: "Docker Research"
---
#### Containers
What are containers?

Containers are a group of processes that run in isolation. All processes must be able to run on the shared kernel.

Each container has its own set of "namespaces" (isolated views), some examples being:
	- PID: process IDs
	- USER: user and group IDs
	- UTS: hostname and domain name
	- NS: mount points
	- NET: network devices, stacks, ports
	- IPC: inter-process communications, message queues

Another feature of the Linux Kernel is the `cgroups`. They allow to monitor and control the resources of the containers.

Other than the Linux Kernel itself, there is nothing special about containers. What makes containers useful is the tooling that surrounds them.

#### Difference between VM and Container
A Virtual Machine comes with a full-blown operating system built into it. On the other hand, Docker Containers use the Base OS/Kernel to run processes. This makes them much faster to run than VMs and are also lightweight. Containers share the same base Kernel.

Containers don't replace Virtual Machines, they can run on top of them. This is often useful to completement the needs of the Virtual Machine.

#### Docker
What is Docker?

Docker is a tooling to manage containers. It simplifies existing technology to enable it for the masses.
It also enables developers to use containers for their application, by packaging dependencies in their containers and enabling the "build once, run anywhere" strategy.

#### The benefits of Containers
- They solve the "But it works on my machine" problem.
- They're lightweight and fast.
- They have better resource utilization. A lot more Containers can fit into a host rather than VMs. => it saves money.
- It provides a standard developer to operations interface: `docker run`.
- Both an ecosystem and tooling exist for Containers.

#### Docker Commands
Use the following command to run your first container:

```bash
docker container run -t ubuntu top
```

This will allow us to run a container with the Ubuntu image. The `-t` flag allocates a pseudo-TTY, which you need for the `top` command to work properly.

The `docker run` command first starts a `docker pull` to download the Ubuntu image onto your host. After its downloaded, it will start the container.

`top` is a Linux utility that prints the processes on a system and orders them by resource consumption.

Use the following command to run bash inside of the Ubuntu container:

```bash
docker container exec -it <containerID> bash
```

The flag `-it` makes it interactive.

You can use the following command to see the running processes inside the Ubuntu container:

```bash
ps -ef
```

