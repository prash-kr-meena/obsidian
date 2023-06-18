
[Never install locally](https://www.youtube.com/watch?v=J0NuOlA2xDc&ab_channel=Coderized)

A container and a container image are related concepts in the world of [[containerization]], but they are not the same thing.

- [[what is a container image?]]
- [[what is a container?]]


In summary
- a container is an instance of a container image that runs an application
- while a container image is a package that contains everything needed to run an application. 
and 
- A container image is used to create containers, which are the actual runtime instances that execute the application.


[[what are containers based on?]]

---
TODO 

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


