Kubenetes Doc from UDemy Course
![[KubernetesForBeginners-MumshadMannambeth.pdf]]



[[Kode Kloud Labs & Slack Community]]
[[Kubernetes For Beginners - Kode Kloud.pdf]]

---

For Understanding Kubernetes, we need to understand 
1. container and 
2. orchestration
Once we get familiarized with both of these terms, we would be in a
position to understand what Kubernetes is capable of.




## Understanding Containers
for understanding containers, we need to understand 
1. [[Virtualization]]
2. [[Containerization]]
3. [[Containers vs Virtualization]]
4. [[What are virtual machines (VMs)| Virtual Machines]]
5. [[Containers & Container Images]]
6. [[Containers vs Virtual Machines]]
7. [[Docker]], which is one of the container engines


----



Section 1

[KUBERNETES ELIMINATES MATRIX FROM HELL](https://www.devsamurai.com/en/kubernetes-eliminates-matrix-from-hell/)
compatibility matrix issue is usually referred to as the matrix from hell.
![[from pdf - matrix of hell.png]]



![[from pdf - what can container do?.png]]

Kubernetes = [[Containers & Container Images|Containers]] + orchestration



Containers are completely isolated environments, as in they can have their own processes or services, their own network interfaces, their own
mounts, just like Virtual machines, except that they all share the same OS kernel.

It's also important to note that containers are not new with Docker. Containers have existed for about 10 years now and some of the different types of containers are LXC, LXD , LXCFS etc. Docker utilizes LXC containers.

Setting up these container environments is hard as they are very low level and that is were Docker offers a high-level tool with several powerful functionalities making it really easy for end users like us.


#### Container Orchestration
So we learned about containers and we now have our application packaged into a docker container. But what next? How do you run it in production? What if your application relies on other containers such as database or messaging services or other backend services? What if the number of users increase and you need to scale your application? You would also like to scale down when the load decreases. 

To enable these functionalities, you need an underlying platform with a set of resources. The platform needs to orchestrate the connectivity between the containers and automatically scale up or down based on the load. This whole process of automatically deploying and managing containers is known as Container Orchestration.


Advantages of Container Orchestration
There are various advantages of container orchestration. Your application is now highly available, as hardware failures do not bring your application down because you have multiple instances of your application running on different nodes. The user traffic is load balanced across the various containers. When demand increases, deploy more instances of the application seamlessly and within a matter of second and we have the ability to do that at a service level. When we run out of hardware
resources, scale the number of nodes up/down without having to take down the application. And do all of these easily with a set of declarative object configuration files.

And THAT IS Kubernetes. It is a container Orchestration technology used to orchestrate the deployment and management of 100s and 1000s of containers in a clustered environment.

## Kubernetes Architecture



Major topics starting points

- [[Pod]]
- [[Deployments]]


then each topics

