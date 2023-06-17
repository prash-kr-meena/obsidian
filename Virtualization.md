From the [Advanced Operating Systems course on Udemy](https://learn.udacity.com/courses/ud189)

# Lectures from Udacity 

## L03a: Intro to Virtualization

### Introduction

![Introduction - Georgia Tech - Advanced Operating Systems](https://www.youtube.com/watch?v=gAuYI7TiXgo)

### Quiz

![Virtualization Quiz - Georgia Tech - Advanced Operating Systems](https://www.youtube.com/watch?v=CovACwT5fMg)

![Virtualization Quiz Solution - Georgia Tech - Advanced Operating Systems](https://www.youtube.com/watch?v=vtjMgvSLqtY)


### Platform Virtualization
![Platform Virtualization - Georgia Tech - Advanced Operating Systems](https://www.youtube.com/watch?v=clxKdltzFXU)

### Utility Computing
virtualization is the logical extension to the idea of extensibility or specialization of services that we have seen in the in the previous lesson, through the spin and exokernel papers.
only now, it is applied at a much larger granularity namely an entire operating system

In other words, virtualization is extensibility applied at the granualarity of an entire operating system as apposed to individual services within an operating system

![Utility Computing - Georgia Tech - Advanced Operating Systems](https://www.youtube.com/watch?v=mm9Xam0DjJQ)

### Hypervisor
Note: *<u>Hypervisor is an Operating system</u>* for the Operating Systems
It is tha manager for all the other virutal machines

These bare metal hypervisors interfear minimally with the normal operations of the guest operating systems on the shared resources (hardware), this is in a spirit which is very familier to the extensible OS that we have studied earlier like the spin and exokernel and therefore the baremetal hypervisors offer the best performance for the guest OS on the shared resources

![Hypervisors - Georgia Tech - Advanced Operating Systems](https://www.youtube.com/watch?v=Q0XyphhfJXE)

### Connecting the dots

![Connecting the Dots - Georgia Tech - Advanced Operating Systems](https://www.youtube.com/watch?v=lBTXJ52639g)



### Full Virtualization

![Full Virtualization - Georgia Tech - Advanced Operating Systems](https://www.youtube.com/watch?v=CLR0pq9dy4g)

![Cloud Computing -Para Virtualization](https://www.youtube.com/watch?v=-rrnt79YPZ4)



### Para Virtualization

![Para Virtualization - Georgia Tech - Advanced Operating Systems](https://www.youtube.com/watch?v=1PYNcmZTjiE)


![Modification of Guest OS Code Quiz - Georgia Tech - Advanced Operating Systems](https://www.youtube.com/watch?v=33U3_wAeSwQ)

![Modification of Guest OS Code Quiz Solution - Georgia Tech - Advanced Operating Systems](https://www.youtube.com/watch?v=lnhFag1x7G4)

![Para Virtualization (cont) - Georgia Tech - Advanced Operating Systems](https://www.youtube.com/watch?v=uoTPmCUfedU)


### Big Picture
![Big Picture - Georgia Tech - Advanced Operating Systems](https://www.youtube.com/watch?v=0T4nRx69b8E)





## L03b: Memory Virtualization
### introduction

![Introduction - Georgia Tech - Advanced Operating Systems](https://www.youtube.com/watch?v=Bq0qVZtd84w)


### Memory Hierarchy
![Memory Hierarchy - Georgia Tech - Advanced Operating Systems](https://www.youtube.com/watch?v=-y9J78wSJHY)

### Todo -- remaining other lecture nee to complete



## L03c: CPU & Device Virtualization








# Lectures from IIT Bombay
[Virtualization and Cloud Computing lectures Playlist](https://www.youtube.com/playlist?list=PLDW872573QAbcpQ7VSUdcm4o3tgnQYBE8)



--

[Full and Para Virtualization - Dr. Sanjay P. Ahuja, Ph.D](https://www.unf.edu/~sahuja/cloudcourse/Fullandparavirtualization.pdf)
Fidelity National Financial Distinguished Professor of CIS
School of Computing, UNF



----

[Virtualization Explained - IBM Technology](https://www.youtube.com/watch?v=FZR0rG3HKIk)
[Virtualization Concept - IBM Technology](https://www.ibm.com/topics/virtualization)

Virtualization (v12n), is a technology that enables the creation of virtual versions of computer hardware, operating systems, storage devices, and networks. It is the foundation of [[Cloud Computing]].

Virtualization began as a method of **logically dividing the system resources** provided by mainframe computers between different applications. This provides a way to efficiently utilize hardware resources and enables applications to run in a more flexible and scalable manner.
Whereas traditionally, these applications would bound to hardware


Virtualization is a concept that is used by [[What are virtual machines (VMs) |Virtual Machines]] and [[what is a container?|container]], hence virtualization allows us to run multiple virtual machines (VMs) or containers on a single physical host machine, **each with its own isolated environment**. 

Virtualization is achived with the help of [[What is a Hypervisor?|hypervisor]]
![Hypervisor based virtualisation](https://blog.risingstack.com/wp-content/uploads/2021/07/hypervisor-based-virtualization.jpeg)


[[Virtualizations Practical Example]]

[[Beneifts of virtualization]]

[[Types of Virtualization]]




Now, regarding the [[Containerization|relationship between virtualization and containerization]]