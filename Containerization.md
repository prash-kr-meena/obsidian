Todo
https://phoenixnap.com/kb/docker-image-vs-container
https://en.wikipedia.org/wiki/Containerization_(computing)
https://www.docker.com/resources/what-container/


[[Containerization]] is a type of operating **system-level virtualization** that allows **multiple isolated user-space (called *container*) instances** to run on a single operating system kernel. 
This operating system kernel can by in any cloud, non-cloud environment, regardless of the type of vendor. (Hence no vendon lock int)


Containers share the same host operating system, but each container has its own
- file system, 
- network stack, and 
- process space. 
In contrast, traditional virtualization involves running multiple virtual machines on a single host, each with <u>its own operating system and kernel</u>.

## Advantages of Containerization
Containerization provides several advantages over traditional virtualization, such as 
- lower overhead, 
- faster startup times, 
- and higher density. 

Containerization also enables the <u>efficient deployment</u> and **scaling of applications**, making it a popular choice for modern application development and deployment.


## Containerization vs Virtualization
It’s easy for one to be confused by the difference between containerization (what containerization software like Docker enables) and traditional <u>server virtualization</u> (what hypervisors like HyperV and VMware ESXi enable). 

In simple terms, the difference boils down to this:

- **Server virtualization** is about abstracting hardware and running an operating system. 
- **Containerization** is about abstracting an operating system and running an app. 
- They both abstract away resources, **containerization is just another level “up” from server virtualization**. In fact, containerization and server virtualization <u>are not mutually exclusive</u>. 
  
  You can run containerized apps on top of a container engine that is deployed within a virtual machine.

![[Pasted image 20230617125108.png]]


---


### What are “containers” and “VMs”?

Containers and VMs are **similar in their goals**: to isolate an application and its dependencies into a self-contained unit that can run anywhere.

Moreover, containers and VMs remove the need for physical hardware, allowing for more efficient use of computing resources, both in terms of energy consumption and ccost-effectiveness

The **main difference** between containers and VMs is in their architectural approach.  as we see above


## Types of containers

- OS containers
- Apps containers

### Security issues

- Because of common OS, security threats can affect the whole containerized system.
- In containerized environments, security scanners generally protect the OS but not the application containers, which adds unwanted vulnerability.

## Container management, orchestration, clustering

Container orchestration or container management is mostly used in the context of application containers. Implementations providing such an orchestration include [[Kubernetes]] and [Docker swarm](https://en.wikipedia.org/wiki/Docker_(software) "Docker (software)").

## Container cluster management

Container clusters need to be managed. This includes functionality to create a cluster, to upgrade the software or repair it, balance the load between existing instances, scale by starting or stopping instances to adapt to the number of users, to log activities and monitor produced logs or the application itself by querying sensors. Open-source implementations of such software include [OKD](https://en.wikipedia.org/wiki/OKD_(software) "OKD (software)") and Rancher. 
Quite a number of companies provide container cluster management as a managed service, like Alibaba, Amazon, Google, Microsoft.

## See also

- [[Docker]]
- [[Kubernetes]]
- [Open Container Initiative](https://en.wikipedia.org/wiki/Open_Container_Initiative "Open Container Initiative")
- [[What are virtual machines (VMs)|Virtual Machines]]
