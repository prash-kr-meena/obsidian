You can understand a Hypervisor as an Operating System for the Operatings Systems

Hypervisor is a small software layer that enables multiple instances of 
[[Operating System - TODO]] to run alongside each other, sharing the same physical computing resources. 

This process is called [[Virtualization]], and the operating system instances are referred to as [[What are virtual machines (VMs)|virtual machines (VMs) ]]— software emulations of physical computers.


Hypervisor is also known as **virtual machine monitor** (VMM) that manages these VMs as they run alongside each other. The hypervisor allocates physical computing resources—such as processors, memory, and storage—to each VM. It keeps each VM separate from others, so they don’t interfere with each other. So if, for example, one OS suffers a crash or a security compromise, the others survive


![Hypervisor || Virtual Machine Manager || Cloud computing](https://www.youtube.com/watch?v=jKQFLXPih3M&ab_channel=K.SEasySolutions)

## Categories of Hypervisor

There are two broad categories of hypervisors: Type 1 and Type 2.

![[Hypervisors and their types.png]]

### Type 1 hypervisor - Bare Metal Hypervisor
  
- A Type 1 hypervisor runs directly on the underlying computer’s physical hardware, interacting directly with its CPU, memory, and physical storage. 
- For this reason, Type 1 hypervisors are also referred to as bare-metal hypervisors. 
- A Type 1 hypervisor takes the place of the host operating system.

##### Advantages of Bare Metal Hypervisors
- Type 1 hypervisors are highly efficient because they have direct access to physical hardware. 
- This also increases their security, because there is nothing in between them and the CPU that an attacker could compromise. 
- But a Type 1 hypervisor often requires a separate management machine to administer different VMs and control the host hardware.
- These bare metal hypervisors interfear minimally with the normal operations of the guest operating systems on the shared resources (hardware), this is in a spirit which is very familier to the extensible OS that we have studied earlier like the spin and exokernel and therefore the baremetal hypervisors offer the best performance for the guest OS on the shared resources


### Type 2 hypervisor - Hosted Hypervisor
- A Type 2 hypervisor doesn’t run directly on the underlying hardware. 
- Instead, it runs as an application in an OS. 
- Type 2 hypervisors rarely show up in server-based environments. Instead, they’re suitable for individual PC users needing to run multiple operating systems. 
	- Examples include engineers, security professionals analyzing malware, and business users that need access to applications only available on other software platforms.

![Type 2 Hypervisor Example](https://www.ubackup.com/screenshot/en/acb/virtual-machine/type-1-hypervisor-vs-type-2/type-2-hypervisor-examples.png)

##### Advantages of Hosted Hypervisor
- Type 2 hypervisors often feature additional toolkits for users to install into the guest OS. 
	- These tools provide enhanced connections between the guest and the host OS, 
	 e.g. they often enable the user to cut and paste between the two or
	 access host OS files and folders from within the guest VM.

- A Type 2 hypervisor enables quick and easy access to an alternative guest OS (VMs OS) alongside the primary one running on the host system. This makes it great for end-user productivity. 
  A consumer might use it to access their favorite Linux-based development tools while using a speech dictation system only found on Windows, for example.


##### Disadvantage of Hosted Hypervisor
- But because a <u>Type 2 hypervisor must access computing, memory, and network resources via the host OS</u>, **it introduces latency issues that can affect performance.** 
- It also introduces potential security risks if an attacker compromises the host OS because they could then manipulate any guest OS running in the Type 2 hypervisor.


![Type 1 Hypervisor vs Type 2 Hypervisor](https://linuxhandbook.com/content/images/2021/11/type1-type2-hypervisor.png)



