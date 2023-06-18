## Containerization vs Virtualization
It’s easy for one to be confused by the difference between containerization (what containerization software like Docker enables) and traditional <u>server virtualization</u> (what hypervisors like HyperV and VMware ESXi enable). 

In simple terms, the difference boils down to this:

- **Server virtualization** is about abstracting hardware and running an operating system. 
- **Containerization** is about abstracting an operating system and running an app. 
- They both abstract away resources, **containerization is just another level “up” from server virtualization**. In fact, containerization and server virtualization <u>are not mutually exclusive</u>. 
  
  You can run containerized apps on top of a container engine that is deployed within a virtual machine.

![[Pasted image 20230617125108.png]]

