
There are different types of virtualization, including:

## 1. Para-virtualization
It is also a part of **Server Virtualization**

In para-virtualization, the hypervisor provides a virtualized hardware interface to each virtual machine, allowing them to share physical hardware resources. This enables better performance than full virtualization, but it requires the guest operating system to be modified.

![Full Virtualization - Georgia Tech - Advanced Operating Systems](https://www.youtube.com/watch?v=CLR0pq9dy4g)

![Cloud Computing -Para Virtualization](https://www.youtube.com/watch?v=-rrnt79YPZ4)


## 2. Full virtualization (or Virtualization)

It comes under the category of **Server Virtualization**

Since a hypervisor or full virtualization mechanism emulates the hardware, **you can run any operating system on top of any other**, Windows on Linux, or the other way around. <u>Both the guest operating system and the host operating system run with their own kernel</u> and the communication of the guest system with the actual hardware is done <u>through an abstracted layer of the hypervisor</u>.


![Hypervisor based virtualisation](https://blog.risingstack.com/wp-content/uploads/2021/07/hypervisor-based-virtualization.jpeg)
*(in the image A hypervisor, also known as a virtual machine monitor or **VMM**, is software that creates and runs virtual machines (VMs))*


This approach usually **provides a high level of isolation** and security as all communication between the guest and host is through the hypervisor. 
This approach is also usually **slower** and **incurs significant performance** overhead due to the hardware emulation.


To reduce this overhead, another level of virtualization called “**operating system virtualization**” or “**container virtualization** (containerization)” was introduced which allows running multiple isolated **user space** instances on the same kernel.

![Cloud Computing - Full Virtualization](https://www.youtube.com/watch?v=wh9ZUxiB2j8)


## 3. Operating system-level virtualization
In operating system-level virtualization, a single operating system kernel is used to run multiple isolated user-space instances, each with its own file system, network stack, and process space. **This is the type of virtualization used by containers.**

## 4. Application virtualization
In application virtualization, applications are encapsulated into virtual containers that include all the necessary dependencies, libraries, and configuration files needed to run the application. This enables applications to run on different operating systems without requiring modification.



## Difference between Para-Virtualization & Full Virtualization

![Full Virtualization vs. Paravirtualization: What's the Difference?](https://www.youtube.com/watch?v=WIPi7l0d8Ww)

