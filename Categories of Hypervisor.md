There are two broad categories of hypervisors: Type 1 and Type 2.

### Type 1 hypervisor - Bare Metal Hypervisor
  
- A Type 1 hypervisor runs directly on the underlying computer’s physical hardware, interacting directly with its CPU, memory, and physical storage. 
- For this reason, Type 1 hypervisors are also referred to as bare-metal hypervisors. 
- A Type 1 hypervisor takes the place of the host operating system.

##### Advantages of Bare Metal Hypervisors
- Type 1 hypervisors are highly efficient because they have direct access to physical hardware. 
- This also increases their security, because there is nothing in between them and the CPU that an attacker could compromise. 
- But a Type 1 hypervisor often requires a separate management machine to administer different VMs and control the host hardware.


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


![[kubenetes/Type1 vs Type 2 Hypervisor.png]]