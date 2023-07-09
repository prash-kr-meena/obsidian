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




[KUBERNETES ELIMINATES MATRIX FROM HELL](https://www.devsamurai.com/en/kubernetes-eliminates-matrix-from-hell/)
compatibility matrix issue is usually referred to as the matrix from hell.
![[from pdf - matrix of hell.png|900]]



![[from pdf - what can container do?.png|900]]

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


![[components on - master vs worker node.png|1000]]

#### Kubectl
We also need to learn a little bit about ONE of the command line utilities known as the kube command line tool or kubectl or kube control as it is also called. 

The kube control tool is used to deploy and manage applications on Kuberneteses cluster, to get cluster information, get the status of nodes in the cluster and many other things.

The `kubectl run` command is used to deploy an application on the cluster. The `kubectl cluster-info` command is used to view information about the cluster, and the `kubectl get pod` command is used to list all the nodes part of the cluster. 
We will explore more commands with kubectl when we learn the associated concepts.


Answer key for my Kubernetes for Beginners Course on Udemy - https://github.com/mmumshad/kubernetes-training-answers
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
![[Pasted image 20230708142403.png|600]]


Below we see the simplest of simplest cases were you have a single node kubernetes cluster with a single instance of your application running in a single docker container encapsulated in a POD. 
![[Pasted image 20230708141454.png|700]]


What if the number of users accessing your application increase and you need to scale your application? You need to add additional instances of your web application to share the load. 

Now, were would you spin up additional instances? Do we bring up a new container instance within the same POD? 

No! We create a new POD altogether with a new instance of the same application. As you can see we now have two instances of our web application running on two separate PODs on the same kubernetes system or node.
![[Pasted image 20230708141750.png|900]]



What if the user base FURTHER increases and your current node has no sufficient capacity? 
Well THEN you can always deploy additional PODs on a new node in the cluster. You will have a new node added to the cluster to expand the cluster’s physical capacity. 
![[Pasted image 20230708141943.png|900]]


SO, what I am trying to illustrate in this slide is that, PODs **usually** have a one-to-one relationship with containers running your application. 

To scale UP you create new PODs and to scale down you delete PODs. You do not add additional containers to an existing POD to scale your application. 


### Multi Container Pods
Now we just said that PODs usually have a one-to-one relationship with the containers, but, are we restricted to having a single container in a single POD? 
![[Pasted image 20230708142450.png|600]]


No! A single POD CAN have multiple containers, except for the fact that they are <u>usually not multiple containers of the same kind</u>. 
As we discussed in the previous slide, if our intention was to scale our application, then we would need to create additional PODs. 

But sometimes you might have a scenario were you have a helper container, that might be doing some kind of supporting task for our web application such as processing a user entered data, processing a file uploaded by the user etc. and you want these helper containers to live along side your application container. 


In that case, you CAN have both of these containers part of the same POD, so that when a new application container is created, the helper is also created and when it dies the helper also dies since they are part of the same POD. 
![[Pasted image 20230708142543.png|800]]

--

The two containers can also communicate with each other directly by referring to each other as `localhost` since they share the same network namespace. 
Plus, they can easily share the same storage space as well.
![[Pasted image 20230708142725.png|800]]


#### Understanding Pods, from a different Angle
We could take another shot at understanding Pods from a different angle. 
Let’s, for a moment, keep Kubernetes out of our discussion and talk about simple docker containers. 

Let’s assume we were developing a process or a script to deploy our application on a docker host. So think of what all steps we would need to do in our script to successfully deploy our app, wrt the scale of our users chaning and the complexity of our application increasing?

So we would first simply deploy our application using a simple `docker run python-app` command and the application runs fine, and our users are able to access it. 
![[Pasted image 20230708143617.png|1000]]


When the load increases, we deploy more instances of our application by running the docker run commands many more times. This works fine and we are all happy. 
![[Pasted image 20230708143748.png|1000]]



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

![[Pasted image 20230708144554.png|1000]]



With PODs, kubernetes does all of this for us automatically. We just need to define what containers a POD consists of and the containers in a POD by default will have access to the same storage, the same network namespace, and same fate as in they will be created together and destroyed together.

![[Pasted image 20230708151130.png|1000]]


Even if our application didn’t happen to be so complex and we could live with a single container, kubernetes still requires you to create PODs. But this is good in the long run as your application is now equipped for architectural changes and scale in the future.

However, multi-pod containers are a rare use-case and we are going to stick to a single container per POD in this course.

### Kubectl
Let us now look at how to deploy PODs. Earlier we learned about the kubectl run command. 

What this command really does is it deploys a docker container by creating a POD. So it first <u>creates a POD automatically</u> and deploys an instance of the nginx docker image. 

But were does it get the application image from? For that you need to specify the image name using the `–-image` parameter. The application image, in this case the `nginx` image, is downloaded from the **docker hub repository**. 
![[Pasted image 20230708152336.png|700]]

Docker hub as we discussed is a public repository were latest docker images of various applications are stored. You could configure kubernetes to pull the image from the public docker hub or a private repository within the organization.
![[Pasted image 20230708152418.png|700]]


Now that we have a POD created, how do we see the list of PODs available? The kubectl get PODs command helps us see the list of pods in our cluster. In this case we see the pod is in a `ContainerCreating` state and soon changes to a `Running` state when it is actually running.
![[Pasted image 20230708152611.png|800]]


Also remember that we haven’t really talked about the concepts on how a user can access the nginx web server. And so in the current state we haven’t made the web server accessible to external users. You can access it internally from the Node though. 

For now we will just see how to deploy a POD and in a later lecture once we learn about networking and services we will get to know how to make this service accessible to end users.

![[Pasted image 20230708152743.png|900]]


### Pods Demo
Started Rancher

`kubectl get all`
```
NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
service/kubernetes   ClusterIP   10.43.0.1    <none>        443/TCP   2d3h
```

`kubectl get pods`
None at this moment


`kubectl run nginxxxx --image=nginx`
```
pod/nginxxxx created
```


`kubectl get all`
```
NAME           READY   STATUS    RESTARTS   AGE
pod/nginxxxx   1/1     Running   0          39s  

NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
service/kubernetes   ClusterIP   10.43.0.1    <none>        443/TCP   2d3h
```

`kubectl get pods`
```
NAME       READY   STATUS    RESTARTS   AGE
nginxxxx   1/1     Running   0          9m24s
```

`kubectl describe pod/nginxxxx`
```
Name:             nginxxxx
Namespace:        default
Priority:         0
Service Account:  default
Node:             lima-rancher-desktop/192.168.5.15
Start Time:       Sat, 08 Jul 2023 15:39:23 +0530
Labels:           run=nginxxxx
Annotations:      <none>
Status:           Running
IP:               10.42.0.14
IPs:
  IP:  10.42.0.14
Containers:
  nginxxxx:
    Container ID:   docker://826d85d5964fb8f8d99f32bd23259ed4ddeae5bfdefd47a835cb73df4f4d057a
    Image:          nginx
    Image ID:       docker-pullable://nginx@sha256:08bc36ad52474e528cc1ea3426b5e3f4bad8a130318e3140d6cfe29c8892c7ef
    Port:           <none>
    Host Port:      <none>
    State:          Running
      Started:      Sat, 08 Jul 2023 15:39:56 +0530
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-xkdm8 (ro)
Conditions:
  Type              Status
  Initialized       True 
  Ready             True 
  ContainersReady   True 
  PodScheduled      True 
Volumes:
  kube-api-access-xkdm8:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type    Reason     Age    From               Message
  ----    ------     ----   ----               -------
  Normal  Scheduled  2m14s  default-scheduler  Successfully assigned default/nginxxxx to lima-rancher-desktop
  Normal  Pulling    2m14s  kubelet            Pulling image "nginx"
  Normal  Pulled     102s   kubelet            Successfully pulled image "nginx" in 31.725216493s (31.725221853s including waiting)
  Normal  Created    102s   kubelet            Created container nginxxxx
  Normal  Started    102s   kubelet            Started container nginxxxx
```
**Note:** The first event is of creating and assigning the pod to the node, which has nothing to do with the image or the container. This is to say the first action of kubernetes is always to first create a pod so that it can then host the containers inside it.


To get additional Information (e.g. The Node and Its Internal IP address)
`kubectl get pods -o wide`
```
NAME       READY   STATUS    RESTARTS   AGE   IP           NODE                   NOMINATED NODE   READINESS GATES
nginxxxx   1/1     Running   0          16m   10.42.0.14   lima-rancher-desktop   <none>           <none>
```



The above demonstration was on how to create a Pod in Kubernetes using the `kubectl run` command, later in this course we will see how to create these Pods using a Yaml Definition

#### Related References
https://kubernetes.io/docs/concepts/
https://kubernetes.io/docs/concepts/workloads/pods/


### Quiz
![[Pasted image 20230708160333.png]]


![[Pasted image 20230708160357.png]]

![[Pasted image 20230708160417.png]]






# Pods / ReplicaSets / Deployments
## Pods

#### Pods With Yaml
Kubernetes uses YAML files as input for the creation of objects such as Pods, Replicas, Deployments, Services etc. All of these follow similar structure. 

A kubernetes definition file always contains 4 top level fields. 
- The `apiVersion`
- `kind`
- `metadata` And 
- `spec`
These are top level or root level properties. These are all **REQUIRED fields**, so you MUST have them in your configuration file.
![[Pasted image 20230708173653.png|500]]


#### `apiVersion`
This is the version of the kubernetes API we’re using to create the object. Depending on what we are trying to create we must use the RIGHT apiVersion. For now since we are working on PODs, we will set the apiVersion as v1. 
Few other possible values for this field are apps/v1beta1, extensions/v1beta1 etc. We will see what these are for later in this course.
![[Pasted image 20230708175925.png|700]]
#### `kind`
The kind refers to the type of object we are trying to create, which in this case happens to be a POD. So we will set it as Pod. 
Some other possible values here could be ReplicaSet or Deployment or Service, which is what you see in the kind field in the table on the right.


#### `metadata`
The metadata is data about the object like its name, labels etc. 
As you can see unlike the first two where you specified a string value, this, is in the form of a dictionary. 

Under metadata, the name is a string value – so you can name your POD `myapp-pod`, and the labels is a dictionary. 
And it can have any key and value pairs as you wish. For now I have added a label app with the value `myapp`. Similarly you could add other labels as you see fit which will help you identify these objects at a later point in time. 
![[Pasted image 20230708180534.png|500]]

Say for example there are 100s of PODs running a front-end application, and 100’s of them running a backend application or a database, it will be DIFFICULT for you to group these PODs once they are deployed. If you label them now as front-end, back-end or database, you will be able to filter the PODs based on this label at a later point in time.

It’s **IMPORTANT** to note that under metadata, you can only specify `name` or `labels` or anything else that kubernetes expects to be under metadata. You **CANNOT** add any other property as you wish under this. *However*, under labels you CAN have any kind of key or value pairs as you see fit. So its IMPORTANT to understand what each of these parameters expect.


#### `spec`
So far we have only mentioned the type and name of the object we need to create which happens to be a Pod with the name `myapp-pod`, but we haven’t really specified the container or image we need in the pod. This is where the last section of this configuration comes in

The last section in the configuration file is the specification which is written as spec. Depending on the object we are going to create, this is were we provide additional information to kubernetes pertaining to that object.
**This is going to be different for different objects**, so its important to understand or refer to the documentation section to get the right format for each. 


Since we are only creating a pod with a single container in it, it is easy. 

Spec is a dictionary so add a property under it called containers, which is a list or an array. 
	The reason this property is a list is because the PODs can have multiple containers within them as we learned in the lecture earlier. 
	In this case though, we will only add a single item in the list, since we plan to have only a single container in the POD. 
	The item in the list is a dictionary, so add a name and image property. The value for image is nginx.


Once the file is created, run the command `kubectl create -f` followed by the file name which is `pod-definition.yml` and kubernetes creates the pod.
`kubectl create -f pod-definition.yaml`

So to summarize **remember the 4 top level properties** `apiVersion`, `kind`, `metadata` and `spec`. Then start by adding values to those depending on the object you are creating.

pod-definition.yaml
```yml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
  labels:
    app: myapp
    type: front-end
spec:
  containers:
    - name: nginx-container
      image: nginx
```

Once we create the pod, how do you see it? 
Use the `kubectl get pods` command to see a list of pods available. In this case its just one. 
To see detailed information about the pod run the `kubectl describe pod` command. This will tell you information about the POD, when it was created, what labels are assigned to it, what docker containers are part of it and the events associated with that POD


### Demo
`kubectl create -f pod-definition.yaml `
```
pod/myapp-pod created
```

`kubectl get pods -o wide `
```
NAME        READY   STATUS    RESTARTS      AGE    IP           NODE                   NOMINATED NODE   READINESS GATES
nginxxxx    1/1     Running   1 (23m ago)   172m   10.42.0.17   lima-rancher-desktop   <none>           <none>
myapp-pod   1/1     Running   0             40s    10.42.0.21   lima-rancher-desktop   <none>           <none>
```

`kubectl describe pod/myapp-pod`
```yaml
Name:             myapp-pod
Namespace:        default
Priority:         0
Service Account:  default
Node:             lima-rancher-desktop/192.168.5.15
Start Time:       Sat, 08 Jul 2023 18:30:54 +0530
Labels:           app=myapp
                  type=front-end
Annotations:      <none>
Status:           Running
IP:               10.42.0.21
IPs:
  IP:  10.42.0.21
Containers:
  nginx-container:
    Container ID:   docker://a48f05618d4a759f86b7d7d761e60ca4c3f00795c6061ffa7a5f0e84de1366ac
    Image:          nginx
    Image ID:       docker-pullable://nginx@sha256:08bc36ad52474e528cc1ea3426b5e3f4bad8a130318e3140d6cfe29c8892c7ef
    Port:           <none>
    Host Port:      <none>
    State:          Running
      Started:      Sat, 08 Jul 2023 18:31:06 +0530
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-gxfhs (ro)
Conditions:
  Type              Status
  Initialized       True 
  Ready             True 
  ContainersReady   True 
  PodScheduled      True 
Volumes:
  kube-api-access-gxfhs:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type    Reason     Age    From               Message
  ----    ------     ----   ----               -------
  Normal  Scheduled  2m55s  default-scheduler  Successfully assigned default/myapp-pod to lima-rancher-desktop
  Normal  Pulling    2m54s  kubelet            Pulling image "nginx"
  Normal  Pulled     2m43s  kubelet            Successfully pulled image "nginx" in 11.186713346s (11.186765569s including waiting)
  Normal  Created    2m43s  kubelet            Created container nginx-container
  Normal  Started    2m43s  kubelet            Started container nginx-container
```



### Questions
**Instruction:** Create a Kubernetes Pod definition file using values below: 

- **Name:** postgres 
- **Labels:** tier => db-tier
- **Container name:** postgres
- **Image:** postgres
```yaml
apiVersion: v1
kind: Pod
metadata:
    name: postgres
    labels:
        tier: db-tier
spec:
    containers:
        -   name: postgres
            image: postgres
```


### Question
**Introduction:** Postgres [Docker image](https://hub.docker.com/_/postgres/) requires an environment variable to be set for password.  

**Instruction:** Set an environment variable for the docker container. **POSTGRES_PASSWORD** with a value **mysecretpassword**. I know we haven't discussed this in the lecture, but it is easy. To pass in an environment variable add a new property '**env**' to the container object. It is a sibling of image and name. **env** is an array/list. So add a new item under it. The item will have properties **name** and **value**. **name** should be the name of the environment variable - **POSTGRES_PASSWORD.** And **value** should be the password - **mysecretpassword**

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: postgres
  labels:
    tier: db-tier
spec:
  containers:
    - name: postgres
      image: postgres
      env:
        -   name: POSTGRES_PASSWORD
            value: mysecretpassword
```



### Labs - Pods
![[Pasted image 20230708201512.png|800]]

#### Familirize with Lab Environment
![[Pasted image 20230708201050.png|1000]]




![[Pasted image 20230708201428.png|1000]]




#### Pods and Yaml

![[Pasted image 20230708201720.png|1000]]


![[Pasted image 20230708201942.png|1000]]


![[Pasted image 20230708202045.png|1000]]

![[Pasted image 20230708202645.png|1000]]


![[Pasted image 20230708202828.png|1000]]


![[Pasted image 20230708203339.png|1000]]

![[Pasted image 20230708203653.png|1000]]

![[Pasted image 20230708203834.png|1000]]

![[Pasted image 20230708204136.png|1000]]

![[Pasted image 20230708204530.png|1000]]


![[Pasted image 20230708205039.png|1000]]

![[Pasted image 20230708205244.png|1000]]

![[Pasted image 20230708205707.png|1000]]

![[Pasted image 20230708205728.png|1000]]






## ReplicaController & ReplicaSet
In this lecture we will discuss about Kubernetes Controllers. Controllers are the brain behind Kubernetes. They are processes that monitor kubernetes objects and respond accordingly. 
In this lecture we will discuss about one controller in particular. And that is the **Replication Controller**.
![[Pasted image 20230708213932.png|900]]


#### So what is a **replica** and why do we need a replication controller? 
Let’s go back to our **first scenario** were we had a single POD running our application. 
What if for some reason, our application crashes and the POD fails? Users will no longer be able to access our application. 
![[Pasted image 20230708214115.png|400]]  ![[Pasted image 20230708214137.png|400]]

To prevent users from losing access to our application, we would like to have more than one instance or POD running at the same time. That way if one fails we still have our application running on the other one. The replication controller helps us run multiple instances of a single POD in the kubernetes cluster thus providing High Availability.

![[Pasted image 20230708214928.png|800]]

#### So does that mean you can’t use a replication controller if you plan to have a single POD?  
No! Even if you have a single POD, the replication controller can help by automatically bringing up a new POD when the existing one fails. Thus the replication controller ensures that the specified number of PODs are running at all times. Even if it’s just 1 or 100.
![[Pasted image 20230708215048.png|300]]


**2nd Scenario**
Another reason we need replication controller is to <u>create multiple PODs to share the load across them</u>. For example, in this simple scenario we have a single POD serving a set of users. When the number of users increase we deploy additional POD to balance the load across the two pods.
![[Pasted image 20230708215311.png|400]]                 ![[Pasted image 20230708215350.png|700]]



If the demand further increases and If we were to <u>run out of resources on the first node</u>, we could deploy additional PODs across other nodes in the cluster. As you can see, **the replication controller spans across multiple nodes in the cluster**. It helps us balance the load across multiple pods on different nodes as well as scale our application when the demand increases.
![[Pasted image 20230708215552.png|1000]]



### Replication Controller And Replica Set
It’s important to note that there are two similar terms. Replication Controller and Replica Set. 
Both have the same purpose but **they are not the same.**
- Replication Controller is the older technology that is being replaced by Replica Set. 
- Replica set is the new recommended way to setup replication. 

However, whatever we discussed in the previous few slides remain applicable to both these technologies. 
There are minor differences in the way each works and we will look at that in a bit.

As such we will try to stick to Replica Sets in all of our demos and implementations going forward.

### Replication Controller
We start by creating a replication controller definition file `rc-definition.yml`.

As with any kubernetes definition file, we will have 4 sections. The apiVersion, kind, metadata and spec. 
- The `apiVersion` is specific to what we are creating. In this case replication controller is supported in kubernetes apiVersion v1. So we will write it as v1. 
- The `kind` as we know is ReplicationController. 
- Under `metadata`, 
	- we will add a `name` and we will call it `myapp-rc`. 
	- And we will also add a few labels, `app` and `type` and assign values to them. 
So far, it has been very similar to how we created a POD in the previous section. 

![[Pasted image 20230708231723.png|400]]            ![[Pasted image 20230708232253.png|500]] 

The next is the most crucial part of the definition file and that is the specification written as `spec`. 
For any kubernetes definition file, the `spec` section defines what’s inside the object we are creating. 

In this case we know that the replication controller creates multiple instances of a Pod. *But what POD?* 
- We create a `template` section under `spec` to provide a Pod template to be used by the replication controller to create replicas. 
- **Now how do we DEFINE the Pod template?** 
  It’s not that hard because, we have already done that in the previous exercise. 
  Remember, we created a `pod-definition.yaml` file in the previous exercise. We could re-use the contents of the same file to populate the template section.
  ![[Pasted image 20230708233613.png|900]]
  
Move all the contents of the `pod-definition.yaml` file into the `template` section of the replication controller, except for the first two lines – which are `apiVersion` and `kind`.  Remember whatever we move must be UNDER the template section. 
![[Pasted image 20230708233715.png|800]]

Looking at our file, 
- we now have two metadata sections – one is for the Replication Controller and another for the POD and 
- we have two spec sections – one for each. 

We have nested two definition files together. The <u>replication controller being the parent</u> and the <u>pod-definition being the child</u>.
![[Pasted image 20230708233926.png|600]]   ![[Pasted image 20230708233953.png|600]]


Now, there is something still missing. We haven’t mentioned how many replicas we need in the replication controller. For that, add another property to the spec called `replicas` and input the number of replicas you need under it. Remember that the template and replicas are direct children of the spec section. So they are siblings and must be on the same vertical line : having equal number of spaces before them.
![[Pasted image 20230708234151.png|500]]

`rec-definition.yml`
```yaml
apiVersion: v1
kind: ReplicationController
metadata:
  name: myapp-rc
  labels:
    app: myapp
    type: front-end
spec:
  template:
    metadata:
      name: myapp-pod
      labels:
        app: myapp
        type: front-end
    spec:
      containers:
        - name: nginx-container
          image: nginx
  replicas: 3
```

Once the file is ready, run the kubectl create command  `kubectl create -f replicaset-definition.yml`

The replication controller Is created. 
When the replication controller is created  it first creates the PODs using the pod-definition template as many as required, which is 3 in this case. 

To view the list of created replication controllers run the `kubectl get replicationcontroller` command and you will see the replication controller listed. 
```
NAME       DESIRED   CURRENT   READY   AGE
myapp-rc   3         3         1       5s
```
We can also see the desired number of replicas or pods, the current number of replicas and how many of them are ready. 

If you would like to see the pods that were created by the replication controller, run the `kubectl get pods` command and you will see 3 pods running. 
**Note :** that all of them are starting with the name of the replication controller which is `myapp-rc` indicating that they are all created automatically by the replication controller.

In my case I was already running one similar pod by name `myapp-pod`, so it did not create the 3rd pod with the name `myapp-rc`
But we can see and confirm that now the `myapp-pod` pod is also being controlled by the Replication Controllers only.

for the cotrast you can check the `nginxxxx` image which I had created earlier, that is not being controller by any sort of Replication Controller
![[Screenshot 2023-07-08 at 11.52.59 PM.png]]

From the Replication Controllers view also we can see, the Current Replicas and Desired Replicas, we can also see the selector that the Replia Controller is using
![[Screenshot 2023-07-08 at 11.54.46 PM.png]]

Upon going into the details of this Replication Controller, we can see its
- `metadata` information:  name, namespace, labels
- `spec` information:  replicas, selectors
- `status`: current replicas, desired replicas etc
- `events`: what all events for the actions executed has been captured
		  we can definetly see and confirm here, that replication controller has only created 2 pods only, and did not create a 3rd pod because already one pod was present (which did not had any owner of it), hence it started controlling it as well as we had the same selector applicable on it as well (and it did not had any owner)
		**NOTE**: We did not actually add this selector in this, and it is generated automatically from the labels, Whereas in ReplicaSet we would mandatorily need to create this selector
![[Screenshot 2023-07-08 at 11.56.56 PM.png|600]]      ![[Screenshot 2023-07-08 at 11.57.56 PM.png|600]]

The above screenshot is basically the UI version of the `kubectl describe replicationcontroller/myapp-rc` command

```yaml
Name:         myapp-rc
Namespace:    default
Selector:     app=myapp,type=front-end
Labels:       app=myapp
              type=front-end
Annotations:  <none>
Replicas:     3 current / 3 desired
Pods Status:  3 Running / 0 Waiting / 0 Succeeded / 0 Failed
Pod Template:
  Labels:  app=myapp
           type=front-end
  Containers:
   nginx-container:
    Image:        nginx
    Port:         <none>
    Host Port:    <none>
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Events:
  Type    Reason            Age   From                    Message
  ----    ------            ----  ----                    -------
  Normal  SuccessfulCreate  12m   replication-controller  Created pod: myapp-rc-m66ls
  Normal  SuccessfulCreate  12m   replication-controller  Created pod: myapp-rc-5tnnc

```


### Replication Set
What we just saw was ReplicationController. Let us now look at ReplicaSet. 
It is very similar to replication controller. As usual, first we have `apiVersion`, `kind`, `metadata` and `spec`. 

The `apiVersion` though is a bit different. It is **`apps/v1`** which is different from what we had before for replication controller. For replication controller it was simply `v1`. If you get this wrong, you are likely to get an error that looks like this. It would say no match for kind `ReplicaSet`, because the specified kubernetes api version has no support for `ReplicaSet`.
![[Pasted image 20230709002920.png|700]]

- The `kind` would be `ReplicaSet` and 
- we add `name` and `labels` in `metadata`.
- The `specification` section looks very similar to replication controller. 
	- It has a template section were we provide pod-definition as before. 
	- So I am going to copy contents over from `pod-definition.yaml` file.
	- And we have number of `replicas` set to 3.


However, there is **one major difference between replication controller and replica set**. 
Replica set **requires** a **`selector`** definition. The `selector` section helps the replicaset <u>identify what pods fall under it</u>. 
But why would you have to specify what PODs fall under it, if you have provided the contents of the pod-definition file itself in the template? 
It’s BECAUSE, replica set can ALSO manage pods that were not created as part of the replicaset creation. 
Say for example, there were pods created BEFORE the creation of the ReplicaSet that match the labels specified in the selector, the `ReplicSet` will also take THOSE pods into consideration when creating the replicas. And then later those pods will be controller by the `ReplicaSet`

Now, This is exactly the same behaviour as we saw in `ReplicationController` as well its just we don't really specify any selector in it (its not mandatory).

![[Pasted image 20230709015921.png|700]]

`replicaset-definition.yml`
```yaml
apiVersion: v1
kind: ReplicationController
metadata:
  name: myapp-rc
  labels:
    app: myapp
    type: front-end
spec:
  template:
    metadata:
      name: myapp-pod
      labels:
        app: myapp
        type: front-end
    spec:
      containers:
        - name: nginx-container
          image: nginx
  replicas: 3
```

And as always to create a `ReplicaSet` run the `kubectl create` command providing the definition file as input 
`kubectl create -f replicaset-definition.yaml`
```
replicaset.apps/myapp-rs created
```

and to see the created replicasets run the `kubectl get replicaset -o wide` command. 
```
NAME       DESIRED   CURRENT   READY   AGE   CONTAINERS        IMAGES   SELECTOR
myapp-rs   3         3         3       41s   myapp-container   nginx    type=front-end
```

To get list of pods, simply run the `kubectl get pods` command.
```
NAME             READY   STATUS    RESTARTS      AGE
nginxxxx         1/1     Running   1 (17h ago)   20h
myapp-rs-27bwq   1/1     Running   0             60s
myapp-rs-29xbp   1/1     Running   0             60s
myapp-rs-c76hd   1/1     Running   0             60s
```


Before we get into understanding these selector, lets solidify the difference between `ReplicationController` and `ReplicaSet`

### Replication Controller Vs Replica Set
<u>The selector is one of the major differences between ReplicationController and ReplicaSet</u>. 
- The selector is **not a REQUIRED** field in case of a replication controller, **but it is still available**. When you skip it, as we did in the previous slide, *it assumes it to be the same as the labels provided in the pod-definition file.* 
	- ie k8s will not fail the creation of Replication Controller Resouce/object if the selector is missing in the menifest, rather k8s will automatcially set the slector for it if not set by the user writing the menifest, and the default value which it will pick is from the `lables` in the pod `template `  
- In case of replica set a user **input is REQUIRED** for this property. And it has to be written in the form of `matchLabels` as shown. 
	- The `matchLabels` selector simply matches the labels specified under it to the labels on the PODs. 
	- The `ReplicaSet` selector also provides <u>many other options for matching labels</u> that were **not available in a replication controller**.
		- ie The selector in Replication Controller is not as powerful as in the Replication Set, specifically the selector supported in RC is equality based selector where ReplicaSet supports both **equality** and **Set** based selectors

To better understand the handson difference between Replication Controller and Replica Set
Watch This video, Great Explaination
 ![25. Kubernetes - ReplicaSet & Diff between Replicaset and Replication Controller](https://www.youtube.com/watch?v=iAxBaTMoRwo&ab_channel=GauravSharma) 
 **Note:** It is recommended that if you are creating a standalone Pod (ie a pod which is not being controller by anyone) then make sure to not add any labels to it, reason being in future if any one introduced some sort of Resoucre that works on selector (eg RC, RS, Deployments) then they might take over that standalone pod and now that resouce has controll over it and can manage it 
 eg. once ReplicaSet got the controll over the standalone Pod, then once we delete the ReplicaSet that Pod will also be deleted, 
       also, it is possible that the traffic that was for ReplicaSet will also reach this Pod



### So what is the deal with Labels and Selectors? Why do we label our PODs and objects in kubernetes?
Let us look at a simple scenario. 
Say we deployed 3 instances of our frontend web application as 3 PODs. 
We would like to create a replication controller or replica set to ensure that we have 3 active PODs at anytime. 
And YES that is one of the use cases of replica sets. <u>You CAN use it to monitor existing pods</u>, if you have them already created. 
And In case they were not created, the replica set will create them for you. 

The role of the replicaset is to monitor the pods and if any of them were to fail, deploy new ones. 
The replica set is in FACT a process that monitors the pods.
![[Pasted image 20230709120829.png|900]]
#### Now, how does the replicaset KNOW what pods to monitor?. 
There could be 100s of other PODs in the cluster running different application. 
![[Pasted image 20230709121222.png|600]]
This is were labelling our PODs during creation comes in handy. 
We could now provide these labels as a filter for replicaset. Under the selector section we use the `matchLabels` filter and provide the same label that we used while creating the pods. This way the replicaset knows which pods to monitor.

This concept of labels and selecters is used in many places throughout kubernetes
![[Pasted image 20230709121349.png|1000]]




Now let me ask you a question along the same lines. 
In the replicaset specification section we learned that there are 3 sections: `template`, `replicas` and the `selector`. 
We need 3 `replicas` and we have updated our `selector` based on our discussion in the previous slide. 
Say for instance we have the same scenario as in the previous slide were we have 3 existing PODs that were created already and we need to create a replica set to monitor the PODs to ensure there are a minimum of 3 running at all times.

When the replication controller is created, it is NOT going to deploy a new instance of POD as 3 of them with matching labels are already created. **In that case, do we really need to provide a template section in the replica-set specification, since we are not expecting the replicaset to create a new POD on deployment?**
![[Pasted image 20230709141916.png|900]]

**Yes** we do, BECAUSE in case one of the PODs were to fail in the future, the <u>replicaset needs to create a new one to maintain the desired number of PODs</u>. And for the replica set to create a new POD, the template definition section IS required.



### Scaling ReplicaSet
Let’s look at how we scale the replicaset. 
Say we started with 3 replicas and in the future we decide to scale to 6. How do we update our replicaset to scale to 6 replicas. 

Well there are multiple ways to do it. 
1. The first, is to update the number of replicas in the definition file to 6. 
  Then run the `kubectl replace` command specifying the same file using the `–f` parameter and that will update the replicaset to have 6 replicas.
  Here it is obivious that the replica inside the manifest (file) has been updated
  ![[Pasted image 20230709142613.png|900]]
  
2. The second way to do it is to run the `kubectl scale` command. 
	- Use the `replicas` parameter to provide the new number of replicas and specify the same file as input.
	  ![[Pasted image 20230709142859.png|700]]
	- You may either input the definition file or provide the replicaset name in the TYPE Name format.
	  ![[Pasted image 20230709142921.png|700]]
  	**However**, Remember that <u>using the file name as input</u> **will not result** in the number of **replicas being updated automatically in the file**. 
       In otherwords, the number of replicas in the replicaset-definition file will still be 3 even though you scaled your replicaset to have 6 replicas using the kubectl scale command and the file as input.

There are also options available for **automatically scaling the replicaset based on load**, but that is an advanced topic and we will discuss it at a **later time**.



### Review Commands for ReplicaSet
Let us now review the commands real quick. 
1. The `kubectl create` command, as we know, is used to create a replica set. You must provide the input file using the `–f` parameter. 
2. Use the `kubectl get` command to see list of replicasets created. 
3. Use the `kubectl delete` replicaset command followed by the name of the replica set to delete the replicaset. 
4. And then we have the `kubectl replace` command to replace or update replicaset and also 
5. The `kubectl scale` command to scale the replicas simply from the command line without having to modify the file.
![[Pasted image 20230709143501.png|1000]]

**Note:** If you are running a ReplicaSet with the replica count of say 3, then if you try to manually create a new Pod which matches the selector specified in the ReplicaSet, what do you think happens?
- You might think that a new Pod will be created along side the old 3 pods but it could be a scenario that this pod will not be controlled by ReplicaSet
- But that is not the case, a new Pod will definetly be created but one of the older pods will be deleted by ReplicaSet as this new Pod will also be controlled by the same ReplicaSet only, and as the ReplicaSet is required to maintain the desired number of Pods, in this case 3 so it will be required to delete the extra pod which is there

### Labs - Replica Set

![[Pasted image 20230709154947.png|800]]

![[Pasted image 20230709155056.png|800]]

![[Pasted image 20230709155342.png|800]]


![[Pasted image 20230709155509.png|1000]]


![[Pasted image 20230709155702.png|900]]

![[Pasted image 20230709155931.png|800]]

![[Pasted image 20230709160107.png|800]]

![[Pasted image 20230709160417.png|900]]

![[Pasted image 20230709161010.png|1000]]

![[Pasted image 20230709161114.png|800]]


![[Pasted image 20230709161501.png|900]]


![[Pasted image 20230709161652.png|900]]

![[Pasted image 20230709161828.png|800]]


## Deployments
![[Pasted image 20230709165123.png|800]]
Say you have a web server that needs to be deployed in a production environment. 
1. You need not ONE, but many such instances of the web server running for obvious reasons.
2. Secondly, when newer versions of application builds become available on the docker registry, you would like to **UPGRADE** your docker instances seamlessly.
3. However, when you upgrade your instances, you <u>do not want to upgrade all of them at once</u> as we just did. This may impact users accessing our applications, so you may want to upgrade them one after the other. 
   And that kind of upgrade is known as **Rolling Updates**.
4. Suppose one of the upgrades you performed resulted in an unexpected error and you are asked to <u>undo the recent update</u>. You would like to be able to **RollBack** the changes that were recently carried out.
5. Finally, say for example you would like to make multiple changes to your environment such as upgrading the underlying WebServer versions, as well as scaling your environment and also modifying the resource allocations etc. 
   You do not want to apply each change immediately after the command is run, instead you would like to apply a **pause** to your environment, make the changes and then **resume** so that all changes are rolled-out together.

All of these capabilities are available with the kubernetes `Deployments`.
![[Pasted image 20230709165812.png|1000]]



![[Pasted image 20230709165927.png|1000]]


So far in this course we discussed about PODs, which deploy single instances of our application such as the web application in this case. Each container is encapsulated in PODs.
![[Pasted image 20230709170058.png|900]]

Multiple such PODs are deployed using Replication Controllers or Replica Sets. 
![[Pasted image 20230709170930.png|900]]

And then comes Deployment which is a kubernetes object that comes higher in the hierarchy. 
The deployment provides us with capabilities to upgrade the underlying instances seamlessly using rolling updates, undo changes, and pause and resume changes to deployments.

![[Pasted image 20230709171020.png|900]]


### Creating a Deployment
As with the previous components, we first create a deployment definition file. The contents of the deployment-definition file are exactly similar to the replicaset definition file, except for the `kind`, which is now going to be `Deployment`.
![[Pasted image 20230709174709.png|400]]      ![[Pasted image 20230709174734.png|400]]

Once the file is ready run the `kubectl create` command and specify deployment definition file. 
![[Pasted image 20230709175517.png|700]]

Then run the `kubectl get` deployments command to see the newly created deployment. 
![[Pasted image 20230709175547.png|700]]

The `Deployment` automatically creates a `ReplicaSet`. So if you run the kubectl get replcaset command you will be able to see a new replicaset in the name of the deployment. 
![[Pasted image 20230709175615.png|700]]

The replicasets ultimately create pods, so if you run the `kubectl get pods` command you will be able to see the pods with the name of the deployment and the replicaset.
![[Pasted image 20230709175644.png|700]]

To see all the created objects at once run the `kubectl get all` command
![[Pasted image 20230709175814.png|800]]

So far there hasn’t been much of a difference between replicaset and deployments, except for the fact that deployments created a new kubernetes object called deployments. We will see how to take advantage of the deployment using the use cases we discussed in the previous slide


### Labs - Deployment
![[Pasted image 20230709182122.png|800]]

![[Pasted image 20230709182222.png|800]]

![[Pasted image 20230709182304.png|800]]

![[Pasted image 20230709182409.png|800]]

![[Pasted image 20230709182529.png|800]]

![[Pasted image 20230709182656.png|800]]

![[Pasted image 20230709182858.png|800]]

![[Pasted image 20230709182956.png|800]]


![[Pasted image 20230709183425.png|800]]

![[Pasted image 20230709183454.png|800]]


![[Pasted image 20230709184248.png|800]]




## Rollout and Rollbacks in a Deployment
In this lecture we will talk about updates and rollbacks in a Deployment.
Before we look at how we upgrade our application, let’s try to understand Rollouts and Versioning in a deployment. 
![[Pasted image 20230709185451.png|900]]

Whenever you create a new `deployment` or **upgrade** the `images` in an existing deployment it triggers a `Rollout`. 
A rollout is the process of gradually deploying or upgrading your application containers. 

When you first create a deployment, it triggers a `rollout`. A new `rollout` creates a new **Deployment `revision`**. Let’s call it  *revision 1*.
![[Pasted image 20230709185653.png|900]]

In the future when the application is **upgraded** – meaning when the container version is updated to a new one
– a new `rollout` is triggered and a new deployment revision is created named *Revision 2*. 
This helps us keep track of the changes made to our deployment and enables us to rollback to a previous version of deployment if necessary.
![[Pasted image 20230709185752.png|900]]


### Rollout Status
You can see the status of your `rollout` by running the command: `kubectl rollout status` followed by the name of the deployment.
![[Pasted image 20230709190014.png|900]]

### Rollout history & Revision
To see the `revisions` and `history` of rollout run the command `kubectl rollout history` followed by the deployment name and this will show you the revisions.
![[Pasted image 20230709190223.png|900]]


### Deployment Strategy
There are two types of deployment strategies. 

![[Pasted image 20230709191617.png|1000]]


Say for example you have 5 replicas of your web application instance deployed.
![[Pasted image 20230709190525.png|500]]
#### Recreate strategy
One way to upgrade these to a newer version is to destroy all of these and then create newer versions of application instances. 
Meaning first, destroy the 5 running instances and then deploy 5 new instances of the new application version.
![[Pasted image 20230709190652.png|1000]]

The problem with this as you can imagine, is that during the period after the older versions are down and before any newer version is up, the application is down and inaccessible to users. This strategy is known as the **Recreate strategy**, and thankfully **this is NOT the default deployment strategy.**
![[Pasted image 20230709191004.png|1100]]


#### Rolling Update
The second strategy is were we do not destroy all of them at once. 
Instead we take down the older version and bring up a newer version one by one. 
This way the **application never goes down** and the **upgrade is seamless**.

![[Pasted image 20230709191041.png|800]]
![[Pasted image 20230709191108.png|800]]


![[Pasted image 20230709191135.png|800]]


![[Pasted image 20230709191157.png|800]]


![[Pasted image 20230709191228.png|800]]

![[Pasted image 20230709191551.png|900]]
Note: One thing that is a little wrong in this diagram is, k8s first deployes the pod with new revision and then will remove older pod, one by one
ie before deletion it first does creation

Remember, if you do not specify a strategy while creating the deployment, it will assume it to be **Rolling Update**. 
In other words, **RollingUpdate** is the **default Deployment Strategy**.



### Updating Deployments
So we talked about upgrades. 

#### How exactly DO you update your deployment? 
When I say update, it could be different things such as
- updating your application version 
- updating the version of docker containers used, 
- updating their labels or updating the number of replicas etc. 

Since we already have a deployment definition file it is easy for us to modify this file. 
![[Pasted image 20230709215458.png|400]]       ![[Pasted image 20230709215529.png|400]]

Once we make the necessary changes, we run the `kubectl apply` command to apply the changes. 
A new `rollout` is triggered and a new `revision` of the deployment is created.
![[Pasted image 20230709215628.png|600]]


#### Another Way to update the Deployment
There is ANOTHER way  to do the same thing. You could use the `kubectl set` image command to update the image of your application. 
But **remember**, <u>doing it this way will result in the deployment-definition file having a different configuration</u>. 
So you must be careful when using the same definition file to make changes in the future.
![[Pasted image 20230709220140.png|600]]


### Recreate vs Rollingupdate Strategy
The difference between the `recreate` and `rollingupdate` strategies can also be seen when you view the deployments in detail. 
Run the `kubectl describe` deployment command to see detailed information regarding the deployments. 

You will notice when the `recreate` strategy was used the <u>events indicate that the old replicaset was scaled down to 0 first</u> and later <u>the new replica set scaled up to 5</u>. 

However when the `rollingUpdate` strategy was used the<u> old replica set was scaled down one at a time</u> **simultaneously** <u>scaling up the new replica set one at a time</u>.
![[Pasted image 20230709220332.png]]


### Upgrades (under the hood)
Let’s look at how a deployment performs an upgrade underthehoods.

When a new deployment is created, say to deploy 5 replicas,
- it first creates a Replicaset automatically, 
- which in turn creates the number of PODs required to meet the number of replicas. 
![[Pasted image 20230709221208.png|700]]
![[Pasted image 20230709221251.png|700]]
![[Pasted image 20230709221338.png|700]]

![[Pasted image 20230709221400.png|700]]

When you **upgrade your application** as we saw in the previous slide, 
the kubernetes deployment object creates a **NEW replicaset** under the hoods and starts deploying the containers there. 
At the same time taking down the Pods in the old replica-set following a `RollingUpdate` strategy.
![[Pasted image 20230709221533.png|700]]
![[Pasted image 20230709221646.png|700]]
![[Pasted image 20230709221719.png|700]]


This can be seen when you try to list the replicasets using the `kubectl get replicasets` command. 
Here we see the old replicaset with 0 Pods and the new replicaset with 5 Pods.
![[Pasted image 20230709221747.png|1100]]


### Rollback
Say for instance once you upgrade your application, you realize something isn’t right. 
Something’s wrong with the new version of build you used to upgrade. So you would like to `rollback` your update. 

Kubernetes deployments allow you to rollback to a previous revision. 
To undo a change run the command `kubectl rollout undo` followed by the name of the deployment. 
![[Pasted image 20230709222349.png|1000]]

The deployment will then destroy the PODs in the new replicaset and bring the older ones up in the old replicaset. 
And your application is back to its older format.
![[Pasted image 20230709222805.png|900]]
![[Pasted image 20230709222842.png|1000]]


When you compare the output of the kubectl get replicasets command, before and after the rollback, you will be able to notice this difference. Before the rollback the first replicaset had 0 PODs and the new replicaset had 5 PODs and this is reversed after the rollback is finished.
![[Pasted image 20230709223132.png|1000]]

### Summarize
To summarize the commands real quick
- use the `kubectl create` command to create the deployment, 
- get deployments command to list the deployments, 
- apply and set image commands to update the deployments, 
- rollout status command to see the status of rollouts and 
- rollout undo command to rollback a deployment operation.
![[Pasted image 20230709223423.png|1000]]


## Demo - Deployment / Rollout / Rollback

`deployment-definition.yaml`
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-deployment
  labels:
    app: myapp
    type: front-end
spec:
  template:
    metadata:
      name: myapp-pod
      labels:
        app: myapp
        type: front-end
    spec:
      containers:
      - name: myapp-container
        image: nginx
  replicas: 6
  selector:
    matchLabels:
      type: front-end
```


`kubectl create -f deployment-definition.yaml`
```
deployment.apps/myapp-deployment created
```


`kubectl rollout status deployment myapp-deployment`
```
deployment "myapp-deployment" successfully rolled out
```

if we ran this command just after we did our deployment we would get the status, output in progress
```
Waiting for deployment "myapp-deployment" rollout to finish: 0 of 6 updated replicas are available...
Waiting for deployment "myapp-deployment" rollout to finish: 1 of 6 updated replicas are available...
Waiting for deployment "myapp-deployment" rollout to finish: 2 of 6 updated replicas are available...
Waiting for deployment "myapp-deployment" rollout to finish: 3 of 6 updated replicas are available...
Waiting for deployment "myapp-deployment" rollout to finish: 4 of 6 updated replicas are available...
Waiting for deployment "myapp-deployment" rollout to finish: 5 of 6 updated replicas are available...
deployment "myapp-deployment" successfully rolled out
```

`kubectl rollout history deployment  myapp-deployment`
```
deployment.apps/myapp-deployment 
REVISION  CHANGE-CAUSE
1         <none>
```

We can observer here that it has one revision which we just did above, 
Note that there is another column called CHANGE-CAUSE, which is `none`, 



`kubectl get deployments`
```
NAME               READY   UP-TO-DATE   AVAILABLE   AGE
myapp-deployment   6/6     6            6           18s
```

`kubectl get replicaset`
```
NAME                          DESIRED   CURRENT   READY   AGE
myapp-deployment-577f5d9dd7   6         6         6       23s
```

`kubectl get pods`
```
NAME                                READY   STATUS    RESTARTS   AGE
myapp-deployment-577f5d9dd7-wt89w   1/1     Running   0          29s
myapp-deployment-577f5d9dd7-44mmf   1/1     Running   0          30s
myapp-deployment-577f5d9dd7-wxsmw   1/1     Running   0          29s
myapp-deployment-577f5d9dd7-hsnk2   1/1     Running   0          29s
myapp-deployment-577f5d9dd7-rmf6r   1/1     Running   0          30s
myapp-deployment-577f5d9dd7-wxcng   1/1     Running   0          30s
```




## Labs - Practice Test - Rolling Updates
## Rolling Updates
### Labs - Services

