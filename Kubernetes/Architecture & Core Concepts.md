# ARCHITECTURE

## CLUSTER
- is made up of a master node and its worker nodes
- 1 network that everything works on

### WORKER NODE
- runs the containers of your application
- similar to a virtual instance / local machine
- contains a pod and proxy/confiq
- multiple worker nodes can be created when scaling up
	
**POD**
	- smallest possible unit
	- holds a container or multiple container
		- usually only 1 container
	- a pod is part of a worker node
	- contains shared resources (e.g volumes) for all Pod containers
	- has cluster internal IP by default
		- communicate via localhost inside a pod
	- pods are ephemeral (stateless)
		- k8 will start or stop or replace as needed
	
**PROXY / CONFIG**
	- to control network traffic on a pod / worker node

**DOCKER**
	- runs in a worker node

 **KUBELET**
	- software needed in a worker node
	- does the communication between master and worker node

**KUBE-PROXY**
	- handles incoming & outgoing traffic
	- whitelisting

### MASTER NODE

#### THE CONTROL PLANE
the control center to control worker nodes

API SERVER
	- most important part of the master node
	- API for the kubelets to communicate

Scheduler
	- watches for new pods, selectw worker nodes to run them on

Kube-Controller-Manager
	- watches and controls worker nodes
	- makes sure correct number of pods

Cloud-Controller-Manager
	- simillar to kube-controller-manager but for cloud provider
	- know how to interact with cloud provider resources

## SERVICES
- Logical group of Pods with a unique, pod- and container-independent ip address
- term for exposing certain pods to the outside world, reachable via certain IP address / domain

### "Deployment" Object
Deployments manage pods for you
	- controller for one or multiple objects
		- user sets a desired state and k8 changes actual state
			- e.g. user defines which pods and containers to run and no. of instances
		- can rollback or pause deployment
		- deployment cab be scaled dynamiclly
			- auto-scaling feature is available

**"SERVICE" OBJECT**
A service object used to expose pods internally and externally
	- a pod's internal IP changes everytime it restarts
	- services groups pods with a shared IP

