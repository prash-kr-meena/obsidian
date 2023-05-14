[Virtualization Explained - IBM Technology](https://www.youtube.com/watch?v=FZR0rG3HKIk)
[Virtualization Concept - IBM Technology](https://www.ibm.com/topics/virtualization)

Virtualization (v12n), is a technology that enables the creation of virtual versions of computer hardware, operating systems, storage devices, and networks. It is the foundation of [[Cloud Computing]].

Virtualization began as a method of **logically dividing the system resources** provided by mainframe computers between different applications. This provides a way to efficiently utilize hardware resources and enables applications to run in a more flexible and scalable manner.
Whereas traditionally, these applications would bound to hardware


Virtualization is a concept that is used by [[What are virtual machines (VMs) |Virtual Machines]] and [[what is a container?|container]], hence virtualization allows us to run multiple virtual machines (VMs) or containers on a single physical host machine, **each with its own isolated environment**. 

Virtualization is achived with the help of [[What is a Hypervisor?|hypervisor]]

[[Virtualizations Practical Example]]

[[Beneifts of virtualization]]

[[Types of Virtualization]]



There are different types of virtualization, including:

1.  Full virtualization: In full virtualization, a hypervisor is used to create multiple virtual machines on a single physical host machine. Each virtual machine runs its own operating system and applications, and they are completely isolated from each other and the host system.
    
2.  Para-virtualization: In para-virtualization, the hypervisor provides a virtualized hardware interface to each virtual machine, allowing them to share physical hardware resources. This enables better performance than full virtualization, but it requires the guest operating system to be modified.
    
3.  Operating system-level virtualization: In operating system-level virtualization, a single operating system kernel is used to run multiple isolated user-space instances, each with its own file system, network stack, and process space. This is the type of virtualization used by containers.
    
4.  Application virtualization: In application virtualization, applications are encapsulated into virtual containers that include all the necessary dependencies, libraries, and configuration files needed to run the application. This enables applications to run on different operating systems without requiring modification.
    

Now, regarding the relationship between virtualization and containerization, containerization is a type of operating system-level virtualization that allows multiple isolated user-space instances to run on a single operating system kernel. Containers share the same host operating system, but each container has its own file system, network stack, and process space. In contrast, traditional virtualization involves running multiple virtual machines on a single host, each with its own operating system and kernel.

Containerization provides several advantages over traditional virtualization, such as lower overhead, faster startup times, and higher density. Containerization also enables the efficient deployment and scaling of applications, making it a popular choice for modern application development and deployment.