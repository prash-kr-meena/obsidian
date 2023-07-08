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

### Concepts
#### Worker Nodes (Minions)
A node is a machine – physical or virtual – on which Kubernetes is installed. A node is a worker machine and this is where containers will be launched by Kubernetes.

It was also known as Minions in the past. So you might hear these terms used inter changeably.

But what if the node on which our application is running fails? Well, obviously our application goes down. So you need to have more than one node.


#### Cluster
A cluster is a set of nodes grouped together. This way even if one node fails, you have your application still accessible from the other nodes. Moreover, having multiple nodes helps in sharing load as well.

#### Master Node
Now we have a cluster, but who is responsible for managing the cluster? Where is the information about the members of the cluster stored? How are the nodes monitored? When a node fails, how do you move the workload of the failed node to another worker node? 

That’s where the Master comes in. The master is another node with Kubernetes installed in it, and is configured as a Master. The master watches over the nodes in the cluster and is responsible for the actual orchestration of containers on the worker nodes.

So every cluster would have one master Node there


#### Kubernetes Components
When you install Kubernetes on a System, you are actually installing the following components. 
- API Server
- etcd service
- kubelet service
- Container Runtime engine
- Controllers and
- Schedulers.

##### API Server
The API server acts as the front-end for Kubernetes. The users, management devices, command line interfaces all talk to the API server to interact with the Kubernetes cluster.

##### ETCD 
etcd is a distributed reliable key-value store used by Kubernetes to store all data used to manage the cluster. 

Think of it this way, when you have multiple nodes and multiple masters in your cluster, etcd stores all that information on all the nodes in the cluster in a distributed manner. 
etcd is responsible for implementing locks within the cluster to ensure there are no conflicts between the Masters.

##### Scheduler
The scheduler is responsible for distributing work or containers across multiple nodes. It looks for newly created containers and assigns them to Nodes.

##### Controllers
The controllers are the brain behind orchestration. They are responsible for noticing and responding when nodes, containers or endpoints goes down. The controllers makes decisions to bring up new containers in such cases.

##### Container Runtime Engine
The container runtime is the underlying software that is used to run containers. In our case it happens to be Docker.

##### Kubelete
And finally kubelet is the agent that runs on each node in the cluster. The agent is responsible for making sure that the containers are running on the nodes as expected.


#### Master vs Worker Node
How are these components distributed across different types of servers. In other words, how does one server become a master and the other slave?

The worker node (or minion) as it is also known, is were the containers are hosted. For example Docker containers, and to run docker containers on a system, we need a container runtime installed. And that’s were the container runtime falls. In this case it happens to be Docker. This doesn’t HAVE to be docker, there are other container runtime alternatives available such as Rocket or CRIO. But throughout this course we are going to use Docker as our container runtime.


The master server has the kube-apiserver and that is what makes it a master.
Similarly the worker nodes have the kubelet agent that is responsible for interacting with the master to provide health information of the worker node and carry out actions requested by the master on the worker nodes.

All the information gathered are stored in a key-value store on the Master. The key value store is based on the popular etcd framework as we just discussed.

The master also has the controller manager and the scheduler.

There are other components as well, but we will stop there for now. The reason we went through this is to understand what components constitute the master and worker nodes. This will help us install and configure the right components on different systems when we setup our infrastructure.


![[components on - master vs worker node.png]]

#### Kubectl
We also need to learn a little bit about ONE of the command line utilities known as the kube command line tool or kubectl or kube control as it is also called. 

The kube control tool is used to deploy and manage applications on Kuberneteses cluster, to get cluster information, get the status of nodes in the cluster and many other things.

The `kubectl run` command is used to deploy an application on the cluster. The `kubectl cluster-info` command is used to view information about the cluster, and the `kubectl get pod` command is used to list all the nodes part of the cluster. 
We will explore more commands with kubectl when we learn the associated concepts.


### Quiz

![[quiz-k8s-udemy-course-72398273.png]]

![[quiz-k8s-udemy-course-20230708133847.png]]


![[Pasted image 20230708134000.png]]


![[Pasted image 20230708134024.png]]

![[Pasted image 20230708134049.png]]

![[Pasted image 20230708134145.png]]

![[Pasted image 20230708134204.png]]


### Pods
With Kubernetes our ultimate aim is to deploy our application in the form of containers on a set of machines that are configured as worker nodes in a cluster. 
However, Kubernetes does not deploy containers directly on the worker nodes. <u>The containers are encapsulated into a Kubernetes object known as PODs</u>. A POD is a single instance of an application. <u>A POD is the smallest object, that you can create in kubernetes</u>.
![[Pasted image 20230708142403.png]]


Below we see the simplest of simplest cases were you have a single node kubernetes cluster with a single instance of your application running in a single docker container encapsulated in a POD. 
![[Pasted image 20230708141454.png]]


What if the number of users accessing your application increase and you need to scale your application? You need to add additional instances of your web application to share the load. 

Now, were would you spin up additional instances? Do we bring up a new container instance within the same POD? 

No! We create a new POD altogether with a new instance of the same application. As you can see we now have two instances of our web application running on two separate PODs on the same kubernetes system or node.
![[Pasted image 20230708141750.png]]



What if the user base FURTHER increases and your current node has no sufficient capacity? 
Well THEN you can always deploy additional PODs on a new node in the cluster. You will have a new node added to the cluster to expand the cluster’s physical capacity. 
![[Pasted image 20230708141943.png]]


SO, what I am trying to illustrate in this slide is that, PODs **usually** have a one-to-one relationship with containers running your application. 

To scale UP you create new PODs and to scale down you delete PODs. You do not add additional containers to an existing POD to scale your application. 


### Multi Container Pods
Now we just said that PODs usually have a one-to-one relationship with the containers, but, are we restricted to having a single container in a single POD? 
![[Pasted image 20230708142450.png]]


No! A single POD CAN have multiple containers, except for the fact that they are <u>usually not multiple containers of the same kind</u>. 
As we discussed in the previous slide, if our intention was to scale our application, then we would need to create additional PODs. 

But sometimes you might have a scenario were you have a helper container, that might be doing some kind of supporting task for our web application such as processing a user entered data, processing a file uploaded by the user etc. and you want these helper containers to live along side your application container. 


In that case, you CAN have both of these containers part of the same POD, so that when a new application container is created, the helper is also created and when it dies the helper also dies since they are part of the same POD. 
![[Pasted image 20230708142543.png]]

--

The two containers can also communicate with each other directly by referring to each other as `localhost` since they share the same network namespace. 
Plus, they can easily share the same storage space as well.
![[Pasted image 20230708142725.png]]


#### Understanding Pods, from a different Angle
We could take another shot at understanding Pods from a different angle. 
Let’s, for a moment, keep Kubernetes out of our discussion and talk about simple docker containers. 

Let’s assume we were developing a process or a script to deploy our application on a docker host. So think of what all steps we would need to do in our script to successfully deploy our app, wrt the scale of our users chaning and the complexity of our application increasing?

So we would first simply deploy our application using a simple `docker run python-app` command and the application runs fine, and our users are able to access it. 
![[Pasted image 20230708143617.png]]


When the load increases, we deploy more instances of our application by running the docker run commands many more times. This works fine and we are all happy. 
![[Pasted image 20230708143748.png]]



Now, sometime in the future our application is further developed, undergoes architectural changes and grows and gets complex. We now have new helper containers that helps our web applications by processing or fetching data from elsewhere. 

These helper containers maintain a one- to-one relationship with our application container and thus, needs to communicate with the application containers directly and access data from those containers.


So For this we would to do some changes in our script, 
- we would need to maintain a map of what app and helper containers are connected to each other, 
- we would also need to establish network connectivity between these containers ourselves using links and custom networks, 
- we would need to create shareable volumes and share it among the containers and maintain a map of that as well. 
- And most importantly we would need to monitor the state of the application container 
- and when it dies, manually kill the helper container as well as its no longer required. 
- Also, When a new container is deployed we would need to deploy the new helper container as well.

- **Note**: I am avoiding networking and load balancing details here to keep the explanation simple, but one can imagine with those concepts a huge amount of work will need to be done in our script 

![[Pasted image 20230708144554.png]]



With PODs, kubernetes does all of this for us automatically. We just need to define what containers a POD consists of and the containers in a POD by default will have access to the same storage, the same network namespace, and same fate as in they will be created together and destroyed together.

![[Pasted image 20230708151130.png]]


Even if our application didn’t happen to be so complex and we could live with a single container, kubernetes still requires you to create PODs. But this is good in the long run as your application is now equipped for architectural changes and scale in the future.

However, multi-pod containers are a rare use-case and we are going to stick to a single container per POD in this course.

### Kubectl
Let us now look at how to deploy PODs. Earlier we learned about the kubectl run command. 

What this command really does is it deploys a docker container by creating a POD. So it first <u>creates a POD automatically</u> and deploys an instance of the nginx docker image. 

But were does it get the application image from? For that you need to specify the image name using the `–-image` parameter. The application image, in this case the `nginx` image, is downloaded from the **docker hub repository**. 
![[Pasted image 20230708152336.png]]

Docker hub as we discussed is a public repository were latest docker images of various applications are stored. You could configure kubernetes to pull the image from the public docker hub or a private repository within the organization.
![[Pasted image 20230708152418.png]]


Now that we have a POD created, how do we see the list of PODs available? The kubectl get PODs command helps us see the list of pods in our cluster. In this case we see the pod is in a `ContainerCreating` state and soon changes to a `Running` state when it is actually running.
![[Pasted image 20230708152611.png]]


Also remember that we haven’t really talked about the concepts on how a user can access the nginx web server. And so in the current state we haven’t made the web server accessible to external users. You can access it internally from the Node though. 

For now we will just see how to deploy a POD and in a later lecture once we learn about networking and services we will get to know how to make this service accessible to end users.

![[Pasted image 20230708152743.png]]