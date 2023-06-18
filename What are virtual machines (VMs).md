A virtual machine is a virtual representation, or emulation, of a physical computer. They are often referred to as a **guest**,while the physical machine they run on is referred to as the **host**.

Each VM runs its own operating system (OS) and behaves like an independent computer, even though it is running on just a portion of the actual underlying computer hardware.


A VM cannot interact directly with a physical computer. Instead, it needs a lightweight software layer called a [[What is a Hypervisor?|hypervisor]] to coordinate between it and the underlying physical hardware.


This technology can go by many names, including 
- **virtual server**, 
- **virtual server instance (VSI)** and 
- **virtual private server (VPS)**, 


## Advantages of Virtual Machines

VMs offer several benefits over traditional physical hardware:

- **Resource utilization and improved ROI**: Because multiple VMs run on a single physical computer, customers don’t have to buy a new server every time they want to run another application or OS, and they can get more return from each piece of hardware they already own.  


- **Scale**: With [[Cloud Computing]], it’s easy to deploy multiple copies of the same virtual machine to better serve increases in load.  
  One can easily scale up or scale down as per the load

**TODO**

- **Portability**: VMs can be relocated as needed among the physical computers in a network. This makes it possible to allocate workloads to servers that have spare computing power. VMs can even move between on-premises and cloud environments, making them useful for [hybrid cloud](https://www.ibm.com/topics/hybrid-cloud) scenarios in which you share computing resources between your data center and a cloud service provider.  

- **Flexibility**: Creating a VM is faster and easier than installing an OS on a physical server because you can clone a VM with the OS already installed. Developers and software testers can create new environments on demand to handle new tasks as they arise.  

- **Security**: VMs improve security in several ways when compared to operating systems running directly on hardware. A VM is a file that can be scanned for malicious software by an external program. You can create an entire snapshot of the VM at any point in time and then restore it to that state if it becomes infected with malware, effectively taking the VM back in time. The fast, easy creation of VMs also makes it possible to completely delete a compromised VM and then recreate it quickly, hastening recovery from malware infections.