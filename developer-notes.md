# Markdown

## Links (files, url)

Include a relative link to a file:
    [a relative link](filepath/url)

## Pictures

To display a picture use:
    ![a relative link](filepath)

# Git

SUPER amazing Git tutorials and articles:
    <https://www.atlassian.com/git/tutorials>

## How To Add Something To Gitignore

**add .env file to .gitignore**
    echo ".env" >> .gitignore

**add all of one type of file to .gitignore**
    echo "*.DS_Store" >> .gitignore

## Get rid of all your changes in a file

    git checkout filename.ext

## Branch Tracking

    git branch -u origin/<branch>

## Updating Your Feature Branch With Changes From Main

There's two main strategies for this:
    1. Rebase on main
    2. Merge main into your feature branch

### Merging Main Into Feature Branches

    git checkout main
    git pull
    git checkout feature-branch
    git merge main
    git push

### Rebasing

**How do you get the new changes from main into your feature branch (in the event your branch is very out of date)?**
    git checkout feature-branch
    git rebase main

    If you have already published your feature branch to remote then:
       git pull --rebase

    Info:
    https://stackoverflow.com/questions/42861353/git-pull-after-git-rebase

**I’m having some weird git issues [git was rejecting pushes of feature2] and now it is clear this is because my two feature branches on the heimdall-client are set to track different things.  One is set to track the remote version of the branch and the other is set to track main.
Which should we set our branches to track?  RN it is like this:
    feature1 tracks remote feature1
    feature2 tracks remote main**

Answer: both branches should track the remote version of themselves.  feature2 should track origin/feature2.

To see what your local branches are tracking use:
    git branch -vv

To see what a single branch is tracking:
    git config --get branch.[branch].remote

If it prints a remote, it's tracking something. If it prints nothing and returns failure, it's not.
    A :  Both branches should track the remote versions of themselves.  feature2 tracks remote feature2, known as origin/feature2

## Creating A New Repo

When creating a repo with github desktop, it generates a new folder of that name to house the repo. So if you want your repo called "resume" and you tell it to generate the repo inside your "resume" folder, inside your workspace, then the path will be "../workspace/resume/resume"

# Terminal / zsh / bash

In mac, cmd + up arrow, takes you to the last command you did, so you can scroll through your history by command.

How to stop a command in terminal (or a program in rhel):
    Ctrl+C

Make nested directories , folders :
    mkdir -p bits/fade/edge/bandwidth/server/

**Information about /usr/ /bin/ /dev/ /lib/ etc in the MacOS filesystem**
A historical sketch of the filesystem hierarchy.  The modern OS X filesystem is documented in the “File System Programming Guide” available on Apple Developer.
    man heir

## history

To see all the history:
    history 0

or:
    less ~/.zsh_history

To check the number of bytes alloted for history:
    echo $HISTSIZE

## which

which – locate a program file in the user's path.

List all executables, not just the first found, for program:
    which -a [program]

## whereis

Similar to which but searches the standard binary as well as manual page directories for program, printing out all paths as it goes.

## PATH

[My PATHs are a mess... How to clean up + very useful commands](https://towardsdatascience.com/my-path-variable-is-a-mess-e52f22bfa520#:~:text=If%20you%20are%20a%20ZSH%20user%20and%20there,UNIX%2C%20you%20can%20add%20multiple%20PATHs%20using%20colons%3A)

## Groups & Users

Show all user accounts only:
    dscl . list /Users | grep -v '_'

View all users and accounts on mac:
    dscl . list /Users

View extensive information on all users:
    dscacheutil -q user

# Regex

Playground for testing: https://regex101.com/

### \w
Any latin letter or digit
### \d 
Any decimal digit
### .
Any character
### [01]
Either 0 or 1 - matches w/ one of the items listed between []
### *
Matches zero or more of preceding character

#### Search "bananna"
    bananna
#### Search for any number of n's in a row
    n*
This matches with "n" and "nn" in "bananna".

#### Search for any word like: bat, bot, bet, bit, but - of any length
    b[aeiou]t
#### Search for any word following b_t pattern, where the _ is any digit
    b[\w]t
#### Any string of the form: digit char digit
    \d.\d
#### Find digits of any length
    \d\d*

## grep

Searches for regex pattern in item specified (file, string, directory).
    grep [options] pattern [item to be searched]

# Linux

## Families of Linux

**Red Hat Family** - Red Hat Enterprise Linux (RHEL), Fedora, CentOS, CentOS Stream, and Oracle Linux.
Uses yum and dnf package managers.

**SUSE Family** - SUSE, SUSE Linux Enterprise Server (SLES), openSUSE.
Uses RPM-based zypper package manager.

**Debian Family** - Debian, Ubuntu, Linux Mint
Uses DPKG-based package manager: apt, apt-get etc. GNOME-based.

## How Linux Works

At the heart of linux is the kernel, which is a program that controls thr computer hardware and directs the processing of programs on it.  The kernel accesses and contorls the keyboard, mouse, cpu, ram, hard drives, and more. Also, technically "Linux" refers to the kernel.

If an outside program, running on the computer wants to access the hardware - for example, play music through a speaker - it interacts through an interface called the syscall, or system call.

### Components the Operating System Manages

**Processes** - linux manages how to divide a program on a multi-core processor
**Memory Management** - linux manages sharing RAM memory between processes, including the allocation and unallocation of RAM memory
**File Management** - makes sure there's enough memory to load files into memory. loads files from disk and back.
**Input/Output** - linux processes requests to hardware (keyboards, monitor, etc) and makes sure the right drivers are there.
**Interpreting User Commands** - use of keyboard and mouse are interpreted so computer acts as expected
**Resource allocation** - the combined management of RAM and processing power, so that all programs have enough memory and processing time to run.

### syscall

The syscall is privileged code which is allowed to make requests to the kernel. It is what user programs use access computer hardware, which must be done via the kernel.

## Features of Linux

Free, Stable (performance does not drop over time), Secure (many security levels available),maintainable (easy to update os and install/uninstall packages), versatile for hardware (runs on many different kinds of computers including appliances), easy to use (it's linux, duh), community supported, open source.

## User Groups on linux (REHL)

To see all the groups you have available:
    groups

To see the groups you have membership of as the root user:
    groups root

To find out your primary group membership:
    $ getent group userName

To see all the users in a group (this one is looking at the docker group):
    grep /etc/group -e "docker"


## Troubleshooting Linux

Problem(s):
    [scottj@b71-int-7002 /opt/scottj/workspace/heimdall-wikis (main)]$ git pull
    @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    @         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
    @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    Permissions 0777 for ‘/home/scottj/.ssh/id_rsa’ are too open.
    It is required that your private key files are NOT accessible by others.
    This private key will be ignored.
    Load key “/home/scottj/.ssh/id_rsa”: bad permissions

Reason this happened:
    I had modified the users on my udev machine when trying to add myself to the docker user group.  They went in and fixed that but then my profile permissions were still unlocked.  To fix it, I did:
        chmod 400 /home/scottj/.ssh/id_rsa

## vi Editor

**How to comment out a text block**
Hit ctrl + v
select lines
shift + i (takes you to insert mode)
Type comment characters
Hit esc

**How to uncomment a text block**
Hit Esc
ctrl + v
use arrows to select above and below and left or right
hit x to delete

**How to undo something in vi/vim**
Hit Esc
hit u

you can use quatifiers to udo multiple changes like this:
3u

3 is used in front to undo last 3 changes.

# HTTP and HTTPS

HTTP is a clearly application protocol that allows the exchange of files on the internet.  It allows web browsers to send requests to web servers and receive and interpret responses.  It operates over the TCP/IP (Transmission Control/ Internet protocol) and QUIC protocols.

HTTPS is HTTP but has SSL a (secure socket layer) added so that the information being transmitted is encrypted.

## HTTP Proxys

An HTTP proxy server acts an intermediarary between the HTTP client and HTTP servers.  Some of the purposes this could serve are speeding up request/response time by filtering requests, protecting the client's IP address, or protecting the main servers from various cyber threats via bad requests.

# Cloud Computing

## Types of Service Models

### IaaS - Infrastructure as a Service

If a business needs a Virtual Machine, then IaaS is the way to go.  This provides compute, data, and network resources to the user in a pay-as-you-go model.  The company or entity using the IaaS handles all of their deployment and allocation needs and the cloud provider supplies the bare resources.  Users: IT Professionals

### PaaS - Platform as a Service

Runtime environments and cloud platforms are provided for users, usually developers, to develop, test, deploy, and manage their environments.  Software engineers can deploy their applications without needing to directly spin up new servers and other IT services.

### SaaS - Software as a Service

Here all software and services are provided and controlled by the cloud provider.  Users pay for access to software such as Microsoft Excel, Gmail, Google Drive, etc.  No IT or software maintenence is required.

![Differences between IaaS, PaaS, and SaaS from Simplilearn](resources/IaaS-PaaS-SaaS.png)

### Private, Hybrid, and Public Clouds

Public clouds are suitable for most users who do not need their data to be separated out and as highly secured as a private cloud.  Services are paid for on an as-needed basis and those resources are owned by the cloud provider.  Private clouds are separated out from all the public cloud computing.  Those private cloud resources belong to the user and are not used by others, as in the public cloud.  Think of public clouds as renting a car, and private clouds as buying a car.

## Cloud Native

Cloud native architecture qualities:
    **Automation** - using testing, CI/CD, git, and other such tools to automate the dev/test/deployment cycle. This could also be automating mantinence or deployment of infrastructure resources. 
    **Self-healing** - infrastructure and apps includes health checks so they can tell if they have stopped working. When these apps or infrastructure resources fail, there is software or scripts to there to automatically redeploy those resources.
    **Scalability** - methods or tools that allow applications and processess to scale automatically.
    **Cost Efficient** - not only do they scale up, they scale down easily and automatically, making it cheaper to operate.
    **Easy to Maintain** - breaking an application into many smaller, single responsibility microservices, allows for work to be spread across teams and updates to be more easily and quickly integrated.  Also makes testing easier.
    **Secure by Default** - using patterns like zero trust computing. Meshes instead of zones?

### The Twelve-Factor App: Guidline for cloud applications

https://12factor.net/

### AutoScaling

Auto-scaling is the dynamic allocation and pruning of resources in response to demand. Kubernetes offers fully automated auto-scaling.

#### Horizontal Scaling

Spawning new instances of an application, allocating more physical servers, and creating more virtual machines are a few examples of horizontal scaling.  This might be creating more kubernetes clusters, more nodes on clusters, or more instances of an application. 

#### Vertical Scaling

Instead of pulling in more server racks to distribute the load across as in horizontal scaling, vertical scaling is increasing the compute power of the servers you are currently using.  Virtual machines and processes can be scaled up by increasing the amount of cpu they have access to.  The upper limit is the physical machines processes are being run on.

**Configuring Scaling** - Configuring scaling involves setting a maximum and minimum of instances, as well as what triggers scaling.

### Serverless Computing

In most other cloud computing models, before an application could be deployed, the infrastructure or development team would need to prepare several resources like networks, load balancers, VMs and operating systems.  These would be needed for even a simple web app.

Instead of managing all those infrastructure and system elements, "serverless" computing lets you simply give the cloud provider your application or script and it determines automatically what resources are needed and allocates them.  Servers are indeed involved but the cloud provider chooses and allocates them.  All cloud providers offer serverless runtimes.

Serverless is sometimes called FaaS (Function as a Service).  Often instead of a company only using serverless systems, they are used in addition to container orchestration and or more traditional IT tools like VMs.  

Small stateless scripts like business logic, events, scheduled tasks and batch processing, is perfect for serverless.

### Open Container Initiative

An open-source organization subset of Linux Foundation that sets standards for container technology.

# Containers

**Why Containers?**
Before containers, the most efficient way to run applications was to spin up virtual machines.  Because these virtual machines however simulate all the parts of a computer, including the kernel of the operating system, they come with a lot of overhead.  Containers solve this problem.

Before containers, system administrators needed to install all the dependencies by hand for a program, making sure all configurations of the network and OS are right for the app.  Containers make is so you easily can specify those dependcy and configuration needs, and the container takes care of it.

## chroot and Isolating Processes

The oldest version of container-like tecnology was the `chroot` command which isolates a process at a particular location from all the other files in the system.  At the location where it is called, a virtual root filesystem is spawned there in the effective chroot jail, locked out from the external files.

Namespaces and cgroups are used in linux to isolate processes and resources even more than chroot can.  Namespaces can be used to isolate resources like a network.

Linux Kernel 5.6 has the following namespaces:
    pid - process ID
    net - allows processes to have their own network, including IP address
    mnt - abstracts the filesystem view and manages mount points
    ipc - inter-process communication provides a seperation for named, shared memory segments
    user - gives a process its own set of user IDs and group IDs
    uts - unix time sharing can give processes a hostname and domain name
    cgroup - allows a process to have its own set of cgroup root directories
    time - virtualizes the clock of the system

Under the hood in docker, namespaces like these are used to isolate the container processes from the rest of the system.

Virtual machines have more overhead than containers because containers are only processes, whereas for a VM you need to simulate all parts of a computer including cpu, ram, hard drive, and an entire operating system.


## Container Storage Interface (CSI), CNI, and CRI

Study Container Storage Interface, Container Network Interfaces, and Containter Runtime Interface for KCNA exam.

## Container Runtimes

If you have an industry-standard container, you don't need Docker to run it.  Only a basic implementation of the OCI runtime-spec standard like runC. Under the hood of Docker, runC is used to start the containers.

Lookup podman as drop-in Docker replacement.

Containers are NOT the same as virtual machines as they share the kernel of the host machine they are run on.  Containers at their core are only isolated processes, an expansion of the abilities of chroot.

VMs have much more overhead, needing much more boot time and resources than containers.  Containers are only processes so they can be started much more quickly than VMs.

Docker follows the Open Container Initiative (or OCI) runtime standards.  OCI implements and maintains a low-level runtime reference called runC.  runC is used by the major container runtimes including Docker.

Container images:  A lightweight executable package of software which contains all the necessary system settings, system tools, dependencies, code, and runtime to run an application.

Docker

-t     Tag flag. Put the tag directly after -t.
-f     File flag. Put path to the Dockerfile you want used directly after -f.

You can use docker to push and pull an image to and from a remote registry, aka a web server where people can upload and download images. 

	docker push myregistry.com/my-image
	docker pull myregistry.com/my-image


Security

When containers are started on the same machine, they share the same kernel.  This creates security concerns if containers are allowed to call kernel functions (for example like killing other processes).  If the container runs as a root user then that opens the door to possibl 


## Podman

Create and start podman VM:
    podman machine init

## Docker

Docker uses containerd to run its containers.  It is built upon it.  So if all you need to do is *start* containers, and not build them, maybe use containerd or another more lightweight runtime in kubernetes, or elsewhere.

### Docker notes from infrastructure

Docker is a broad set of technologies that are used to work with containers. Docker has it's own container runtime, and that is what I am use to. However, Kubernetes (k8s) is depreciating docker as a runtime within it's environment. You might want to look into using other container runtimes than docker, such as containerd or cri-o to build your image. I know docker, so that is what I'll use as an example, and other container runtimes should be very similar if not identical commands.
Docker is what you would use to create an image. You can think of an image almost like a mini computer. It's what we load into the k8s container which runs in a k8s pod.
[This is a good docker sample](https://docs.docker.com/get-started/02_our_app/). You can see the file, as well as how to build it and run it. There is a lot of information there, and you could spend a summer just learning docker (don't do that).
Once you have an image, the goal is to get the image on the the k8s cluster. A normal process would be to tag the image and then push it to a repository such as docker-registry or nexus. I'm familiar with nexus because we are on a close network and don't have open source platforms to utilize. You will want to build the docker image such that the name contains what repo it is suppose to go to, along with an identifying tag. Then push it to that repo.
    docker built -t nexus-repo/serviceABC:v1
    docker push nexus-repo/serviceABC:v1
Now the image is in a location that you can access it from your k8s cluster and will pull it during the creation of your k8s deployment/pods. This is an important piece of the puzzle.

### The DockerFile

You can build an image with only the FROM command.
Only one CMD is run, the very last one specified in the file.  This is run after the container image is started.

#### COPY vs ADD

Both COPY and ADD copy files and directories, along with their contents into the image.

ADD however has extra features where it can also fetch tar archives from a URL and unpack them.  COPY is generally prefered if you are only wanting to move files.  Always use COPY when you don't need extraction.

BEST practice is to avoid ADD entirely and use `RUN curl` etc.

#### 

### Building the image

    `docker build -t name-of-app .`

### Docker CLI

Run containers with simple:
    docker run nginx

All the docker commands:
    docker help

Stop docker container:
    docker ps
    docker stop [processID]

See all current running docker containers:
    docker ps

See all images docker runtime has access to:
    docker images

Remove a specific image:
    `docker rmi -f [containerID]`

Remove all dangling images (old extras from the same build):
    docker rmi -f $(docker images -f dangling=true -q)

Remove a specific image by tag:


### Docker Security

If you start multiple containers on the same machine, they will all be using the same kernel, which is a security risk.  
Best Practices:
    DON'T run containers as root(UID 0) unless absolutely necessary - more secure with non-root user
     - make sure user you run container with exists inside the container
     - don't forget to change USER to a non-default user
    One container per "machine"
    DON'T bind to specific UID - don't use a hardcoded path for tmp data
        `
        USER myuser
        ENV APP_TMP_DATA=/tmp
        ENTRYPOINT ["/myapp"]
        `
    Make all executables owned by root and not writable - blocks the executing user from modifying existing binaries or scripts
        - effectively enforces container immutability, preventing someone from injecting code by modifying the executables
        - without that, the application could be modified *after* runtime
    
    Use Multistage building methods 
       - helps make containers smaller by copying in only the necessary artifacts of a build into the final image
         - I believe this means: example is java app, after maven build, copy in *only* the class files, and dependencies, etc that the jvm needs to run it. Leaving out original code the javabytes were compiled from.


### Docker Troubleshooting

Problem:
    Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?

Solution 1: Start Docker service with Docker Desktop. Open Docker Desktop. Problem solved.

    
# Container Orchestration Fundamentals

Kubernetes is a container orchestration system.  Most orchestration systems, including kubernetes, consist of two parts: the control plane, which manages the containers, and the worker nodes, where the containers are run.

Container Orchestration systems provide a way of building a cluster from multiple servers and allowing containers to be hosted on top. This provides the environment to run modern microservice architecture, which is an application comprised of many independent single-responsibility containers.

Things a Container Orchestration System must do:
    - Provide computing resources like virtual machines that containers can run on
    - Schedule containers to servers in an efficient way
    - Allocate resources like CPU and memory to containers
    - Manage availability of containers. Schedule them if they fail.
    - Scale containers if load increases. And down scale things if load decreases.
    - Provide a network for connecting the containers
    - Provision storage if containers need data persistence


## Networking

Microservice archetecture depends heavily on network communication.  A Microservice implements an interface which can be called to make a request. An example would be a service which responds with a playlist based on a selected artist.  Network namespaces are used to allow each container to own a unique IP address. 

Virtual networks and network namespaces allow containers to have unique IP addresses, but still be connected by a common network that allows easy access from the outside.

Network namespaces allow multiple applications to open the same port, while still allowing them to have a unique IP address.

A virtual network is overlaid across multiple host systems to allow inter-container-communication.

https://github.com/containernetworking/cni

### Service Discovery

**Service Discovery**
The process of finding other services in a network and requesting information about them.

Two approaches to service discovery exist:
    Modern DNS servers - a service API is used to register new services as needed with the DNS server.
    Key-Value-Store - A highly consistent datastore is used to store information about services. ex: etcd

**Service Registry** 
Where all the information about containers and/or servers is stored.

### Service Meshes

Service meshes are used to manage all that traffic between containers, as well as all the settings, proxies, and security measures like encryption.

When you have hundreds or thousands of containers, managing all of the unique IP addresses, the encryption and security measures, and setting up proper routing would be insurmountable.  Service Meshes allow for automation of these processes.

The **Service Mesh Interface** is a standard for service meshes which focus on those that run on Kubernetes.

(Service Mesh Interface Spec)[https://github.com/servicemeshinterface/smi-spec]

Instead of implementing all the functionality needed like: monitoring, routing, filtering, access control, encryption, and more, within your applications, a second container is started called a "proxy" and the proxies handle all these functions.

The service mesh allows these proxies to be started up and configured automatically so that you don't have to do it for every single container.

Examples of Proxies: nginx, haproxy, envoy

Examples of Service Meshes: Istio, linkerd 

When service meshes are used, containers don't talk directly with each other.  Instead, all traffic is routed between the proxies.


# Kubernetes

- High availability or no downtime
- Scalability or high performance - it automatically adjusts to work load
- Disaster recovery - when things go down, we can get them back - backup and restore
- Made of *at least* 1 master node and a couple worker nodes. Each worker node has a kublet process running on it. 

![Kubernetes Architecture diagram made by myself](kubernetes-cluster.jpeg)

Kubernetes allows you to run your applications remotely and scale up your services automatically as your demand grows, or automatically redeploy and replace a service node if one dies.  Once you have a cluster, the Kubernetes Deployment Controller watches your Kubernetes cluster and repairs nodes if they break, or replaces them when they die.  The Controller uses the configmaps of your service to deploy and redeploy your service.  The deployment configuration gives kubernetes instructions on how to redeploy your service.

Kubelet is a kubernetes process that makes it possible for the cluster to talk to itself and for tasks to be executed on worker nodes.
Master node runs processes that are critical to cluster managment.  One such is the API Server which is what you talk to the cluster through.  This includes the CLI and the APIs that are the entry-points into the cluster.

Another running on the master node is the Scheduler, which decides which worker node the next job should be run on.

On the master node there is also a ETCD, backup store, which takes snapshots of the cluster state so if anything goes wrong, the cluster can restore itself to a former state.  If you lose your master node, you lose all access to your cluster, so often they have multiple master nodes, or backups of the node, so it can be restored if something goes wrong with the master.

The master node itself is a container running.  And also inbedded in the cluster is the virtual network, which allows the cluster's nodes to communicate and functiton as one, powerful computer.  Usually the worker nodes are much bigger and require more resources than the master node(s) because they are the ones running the applications.

Each pod, the smallest unit in kubernetes, runs one application.  Each pod has a unique IP address which can be used to access it.  However that unique IP vanishes if the pod dies which is why you can give them a service IP address which is permanent.  The IP given by the Service IP is often messy however which is where Ingress comes in.  Kubernetes uses Ingress to alias and route requests in. So you can turn: http://127.9.0.101:7070 into http://my-app/

## Control plane

**Services running on control plane node**
    kube-apiserver :  The kubernetes api server is THE most important element of a cluster.  Loose access to this and your cluster loses it's ability to communicate with itself.  All requests from all parts, inside and outside the cluster, go through the api server.  All compononents interact with each other through the api server. 

    etcd : etcd is a database that kubernetes uses to keep track of pod and various cluster information.

    kube-scheduler : In charge of choosing appropriate worker nodes for new workloads being scheduled.  It evaluates things like CPU and memory.  If it cannot find an appropriate node, it continues looking until one eventually becomes available.

    kube-controller-manager :  Comprised of non-terminating control loops that manage the sate of the cluser.  Ex: one checks that the desired number of an application are always available.

    cloud-controller-manager(optional) :  Used to interacted with APIs of cloud providers. Ex: create external resources like load balancers, storage, or use security groups.

What happens if the control plane has only one main node and it fails?  Then: https://tinyurl.com/yc7k9haa

### kube-apiserver

A RESTful interface exposed over HTTP by default, but can be set up to be HTTPS.
A container service running on kubernetes.
The front-end of kubernetes resposible for all communication and processing all requests, inside and outside the cluster.

Validates in 3 stages all requests, before processing them:
    1) Authentication: proving you are who you say you are. Can be done with certificate or external identity management. Kubernetes users are *always* externally managed.
    2) Authorization: deciding what the requester is allowed to do. Role Based Access Control(RBAC)
    3) Admission Control: controllers can be used to modify or validate the request.  Ex: user tries to use container from untrusted registery.  admission controller blocks request.  Open Policy Agent can be used to manage control externally.

### kube-scheduler

Makes the decision of what node to start a job on but does not actually start the job.  Continues to look for an appropriate node based on the specifications in the configmap until one is found.

## Worker nodes

Their behavior is completely controlled by the control plane.  If a container or pod is started, that is fully determined by the control plane, through the api server.
In other words, these worker nodes take orders and execute them, reporting issues back.  They don't make any decisions whatsoever.
Because every decision is dictated through the kube-apiserver, if the control plane goes down, nodes with containers running will stay running.

**Components of a worker node**
    container runtime :  runs containers on worker node. containerd is popular since Docker has been depricated.

    kubelet :  small agent that talks to the api-server and container runtime. kubelet gets a list of pods it needs running from the api-server. Then it starts them with the container runtime.  kubelet also does: reporting status of nodes to etcd, help node join a cluster, work on pod spec, and run health checks on pods.

    kube-proxy : A network proxy that handles inside and outside communication of your cluster. Instead of managing traffic flow on it’s own, the kube-proxy tries to rely on the networking capabilities of the underlying operating system if possible.

**Container Runtime Interface**
    specifies a standard to allow containers other than docker ones to be run on kubernetes. circa 2016



## namespaces

A way to organize pods and resources in a cluster.  Grouping services into different namespaces, does NOT isolate their containers.

## Volume

Since kubernetes revolves around easily replicating and replacing pods if they die, if you running a database there, you could easily lose your data if its pod dies.  For this reason Kubernetes lets you attach a volume to pods to backup data.  Using volumes, kubernetes attaches physical, hard-drive storage to your pods.  This can be on the same machine the pod is running on, or a remote server outside the cluster.

## Deployments and Stateful Set

Kubernetes is all about replicability.  Usually in production you would have replicas of an app running on different nodes, on different servers, that way if one goes down you have another running in already to replace it.  The service would connect these, routing requests through the service IP address and DNS. This is how the service is a load balancer.  It routes requests between the various app replicas to distribute them efficiently.

Deployments not pods:  Kubernetes users and admins work with deployments, which specify how many replicas you need.  Deployments are used to create pods, rather than a person hand creating each pod.

For a database however, all the pods running it need a mechanism for connecting which is why it's important to use stateful set to create them, not deployments. Statefulsets are for anything that requires to maintain its state including stateful apps.  It's much harder to set up statefulsets in kubernetes though which is why DBs are usually housed outside a Kubernetes cluster.

## Kubernetes Objects

Mostly abstract resources, called objects, can be used to describe how your workload will be handled.  Kubernetes objects are different than infrastructure objects, which are used for configuration, networking, and security.  And they also differ from workload-oriented objects that handle container workloads.

Some problems the different kubernetes objects address:
    container orchestration
    scheduling
    self-healing
    handling issues from containers

The 5 required fields of a kubernetes object yaml:
    apiVersion: each object is versioned
    kind: the kind of object
    metadata:
        name: required "name" subfield for object must be unique (namespaces can be used if you need multiple deployments with same name)
    spec:
        - desired state

Creating, modifying or deleting objects creates a record of intent.  The kubernetes system takes it from there and does the work to start pods and containers.

**List all kubernetes objects**
    $ kubectl api-resources

## Pods

The most basic unit in kubernetes, an object. A pod is like a wrapper around a container.

How are containers started?  kubelet defines a pod and uses the CRI spec to communicate with the container runtime interface and then it starts the container inside that pod.

## Workload Objects

Variations on pods, slightly more to them.

ReplicaSet
 - A controller object that makes sure the specified number of pods of your application are running. 

Deployment
 - The most feature-rich object in kubernetes.  Deployments are used to describe a complete app lifecycle, by managing ReplicaSets.  Get updated when application is updated with new container image. Great for stateless applications.

StatefulSet
  - databases and other applications which can't be replaced if they fail by creating a new pod. Retain IP addresses

DaemonSet
  - Makes sure copy of pod runs on all(or some) nodes. Ex: infrastructure tools like monitoring or logging

Job
  - like lambda, creates pod(s) that execute your script and terminate afterwards. Ex: database migrations, admin tasks

CronJob
  - Like a job, but can be set to run periodically. Ex: once per night a script scans the database, doing admin/cleaning work

## Networking Objects

### Services

Services are used to expose pods to the outside world.  There are 4 service types:
    ClusterIP - most common type is a virtual IP in k8s that forms a single endpoint for multiple containers
    NodePort - extends cluster IP by adding routing rules. Opens port on every node in the cluster and maps it to the ClusterIP. For external traffic making it to the cluster.
    LoadBalancer - extension of NodePort
    ExternalName - aliases external IP addresses for traffic exiting the cluster.

### Ingress

Ingress Objects allow you to expose pods to the outside and use HTTP/HTTPS.  Ingress configures routing rules via the Ingress Controller.

### NetworkPolicy

K8s automatically supplies a internal cluster firewall which you can configure via the NetworkPolicy. Rules might apply to incomming(ingress) or outgoing traffic(egress).

## ConfigMaps

ConfigMaps are APIs that store configuration data in key-value pairs.  Their primary function is abstract the configuration for a container image away from the image itself.  A config map can contain the entire configuration for the image, or only individual properties.

ConfigMaps help keep an application portable which is important if your goal is to run something in Kubernetes.  Keeping the configuration settings seperate from your application code helps keep your application image light and portable.

With the configuration abstracted away, you can easily adjust properties depending on your environment, allowing easier transition between development, testing, and production.

Are ConfigMaps secure?  They are NOT encrypted and should never contain any sensitive information.  NO passwords, etc.

**Creating a ConfigMap**

You can create a configmap from files, directories, and literal values.

Creating a ConfigMap from a file or literal:
    kubectl create configmap [configmap_name] [attribute] [source]

Depending on the source, the attribute will be:
    --from file (if the source is a file/directory)
    --from-literal (if the source is a key-value pair)

More ways and details: <https://phoenixnap.com/kb/kubernetes-configmap-create-and-use>

**Viewing Config Maps**
To see details from a Kubernetes ConfigMap and the values for keys, use the command:

    kubectl get configmaps [configmap_name] -o yaml

**Configuring a Pod to Use a ConfigMap**
The two ways to configure a pod to use a ConfigMap are:
    - Mount the ConfigMap as a volume
    - Use environment variables

**What is hostPort and hostIP?**
<https://stackoverflow.com/questions/63691946/kubernetes-what-is-hostport-and-hostip-used-for>

## Kubectl

Now that you have your helm charts installed into k8s, you can see your service within the cluster.
    kubectl get deployments
    kubectl describe deployment deployment-name
    kubectl get pods
    kubectl describe pod pod-name
    kubectl get services
    kubectl describe service service-name
    kubectl exec pod-name -- ls /  (executes commands within your pod for testing)
    kubectl exec -it pod-name -- /bin/sh (allows you to enter into a shell in your image for testing)
    curl service-name:80 (hit your application)

There are a lot of kubectl commands you may want to use, but those will get you started.
You may want to look into setting up a "NodePort" service instead of a "ClusterIP" service to allow you to hit your pods from outside of the cluster. Do some research and then ask questions later on if needed.
Pipeline
Whatever you are doing by hand to build your application, test it, and deploy it should be captured in the pipeline. That way you can focus on writing code and making changes. As soon as you push out a change, it all happens automagically and your hotness is in the cluster without you having to do anything.

Cheat Sheet: <https://kubernetes.io/docs/reference/kubectl/cheatsheet/>

Enter Kubernetes cluster:
    ssh kctl-intern1

Exit (use either of the following):
    ~.
    exit

Get info about the kubernetes cluster:
    kubectl get services
    kubectl get pods -n beta
    kubectl explain pods
    kubectl explain nodes

See all the configmaps for the cluster:
    kubectl describe configmaps

See them in yaml format:
    kubectl get configmaps -o yaml

force apply a new configmap:
    kubectl apply -f new-config.yaml

force apply a new configmap to a particular namespace:
    kubectl apply -f memory-request-limit.yaml --namespace=mem-example

see the ip address of your pods:
    kubectl get pod -o wide

see what ports are exposed:
    kubectl get svc --all-namespaces

**How a Kubernetes Pod Gets an IP Address**
<https://ronaknathani.com/blog/2020/08/how-a-kubernetes-pod-gets-an-ip-address/>

## Practicing With Minikube

Starting two nodes in minikube:
    minikube start --nodes 2

Stopping/deleting all minikube clusters:
    minikube delete --all --purge



# Deployment

Build jar:
mvn clean package -Dquarkus.package.type=uber-jar

Helm package:
helm3 package heimdalservice-chart

Send helm file
scp heimdalservice-chart-0.1.0.tgz  kleine@kctl-intern1:hello-world

Build docker image:
docker build -f heimdall-service/src/main/docker/Dockerfile.jvm -t nexus-trunk.udev.six3/heimdall-service .

Push docker image to nexus:
docker push nexus-trunk.udev.six3/heimdall-service

Enter Kubernetes cluster:
ssh kctl-intern1

Uninstall old helm charts:
helm uninstall -n beta heimdall-service

Install new helm charts:
helm install heimdall-service heimdallservice-chart-0.1.0.tgz -n beta

## Pipeline Variable Scopes

Variables declared inside the .gitlab-ci.yml CAN be accessed inside the pom.xml and settings.xml files.  Such pipeline variables must be all caps.

Variables declared inside the pom.xml inside the `<properties></properties>` tag CAN be used inside the .gitlab-ci.yml, pom.xml, and pipelines.

Variables declared on gitlab.com CAN be used inside the pom.xml, settings.xml and the pipeline .gitlab-ci.yml.

## Default Variables For Pipelines

Gitlab has many default variables available for use. Here is a link to them: <https://docs.gitlab.com/ee/ci/variables/predefined_variables.html>

You can use these anywhere inside the pom.xml, settings.xml and .gitlab-ci.yml.

To see all the values available to you inside your runner use:

    stages:
    - debug

    print-all-env-vars-job:
    stage: debug
    script:
        - echo "GitLab CI/CD | Print all environment variables"
        - env

## Notes From Infrastructure On Builds and Pipelines

A sample project could look something like this:
    - serviceABC/
    - serviceABC/biz/ <- holds actual logic that you write println("Hello, World!")
    - serviceABC/helm-charts/ <- kubernetes charts with values.yaml file
    - serviceABC/service/ <- framework such as spring boot that your biz logic would be inserted into
    - serviceABC/tests/ <- automated tests
    - serviceABC/.gitlab-ci.yml <- pipeline definition


### Helm

Helm is pretty simple. It's not just made for k8s, but it's what is used by everyone I've ever known that deploys into k8s. You can use helm for anything that needs search/replace and version control. Helm is a VERY fancy search/replace tool that also gives you the ability to rollback to previous versions of your k8s deployment. You could in theory create your k8s files, and then "apply" those files by hand one by one. Depending on how big your deployment is, that could be a giant pain. Or you could bundle all of your k8s files together into a single helm chart and push it to a k8s cluster. And better yet, you can make it so your chart can deploy onto multiple k8s clusters and vary the details of of the deployment (name, cpu, etc) it's using in the values.yaml file. Now you can see why helm is so helpful.
Quick note, make sure that you are using version 3 of helm (helm3). Helm2 will require you to have a tiller within your k8s namespace, and it's just a hassle. I know you prob don't know what I'm talking about, and that's fine. Just use helm3. If you really care, google it.
    helm version
    helm create serviceABC
    ls -1 serviceABC

- charts <- Dependent charts. You prob wont need this.
- Chart.yaml <- Define your chart (name, version, description, etc). Metadata on your chart.
- values.yaml <- File that holds values to be replaced into the template files below. Substitute values files to quickly change your flavor of deployment.
- templates <- The good stuff.
  - deployment.yaml <- populate this
  - service.yaml <- populate this
  - hpa.yaml <- prob don't need
  - serviceaccount.yaml <- prob don't need
  - ingress.yaml <- prob don't need
  - NOTES.txt <- prob don't need
  - _helpers.tpl <- prob don't need
  
The deployment is where you will define your pods. With what little time you have, I would focus on that. The service is pretty much a load-balancer for your pods and you will want that as well. It is going to be within the pod definition within your deployment that you will define what image to use to run within your pod container. You will want to define that in your values file. I think I saw you guys are already doing that.
However, the hpa, serviceaccount and ingress files are for advanced configuration, so I wouldn't worry about those. The _helpers.tmp file is for advanced usage of helm. If you guys have time to learn how to define Go templating in that file than great. But I won't worry about it.
Now that you have your charts filled out, move the files to your cluster and install them.
    tar -zcvf serviceABC.tgz serviceABC/
    scp serviceABC.tgz user@cluster:/tmp
    ssh user@cluster
    helm install serviceABC /tmp/serviceABC.tgz
    You can get fancy and add flags such as:
    helm -n namespace123 upgrade --install serviceABC /tmp/serviceABD.tgz -f /tmp/special-values/values.yaml --set image=nexus/your_image:v10 --wait --timeout 600s

The above command will upgrade your service if it already exists (so you don't have to delete it first) or will install it if it doesn't already exist. It also is pointing to a special v--set values that overrides the values file that was just used. It also waits for the deployment to finish instead of kicking it off and returning right away, but will mark it as failed after 500 seconds.

#### Install the latest version of Helm
 
    $ curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
    $ chmod 700 get_helm.sh
    $ ./get_helm.sh


### Configuring the Gitlab Runner

Within the /etc/gitlab-runner/config.toml file that describes the runners configuration, you can define mounts that will be available to the executor when they spin up to execute a job. If you want docker to be able to run within the container and run docker commands, you will need to mount the docker executable and the docker socket that allows the server-side daemon to communicate with its cmd line interface. The volumes will look like this in your runner config.
volumes = ["/usr/bin/docker:/usr/bin/docker", "/var/run/docker.sock:/var/run/docker.sock", "/cache"]
I also ran into an issue infrastructure helped with when initially setting this up where I had to flush the nat iptable and re-create the docker bridge. I'll include this just in case you run into this as well.
    pkill docker
    iptables -t nat -F
    ifconfig docker0 down
    ip link delete docker0
    service docker start

# AWS

## Root vs IAM users

Root user has access and full control of everything.  Do not use the Root user account for daily tasks.  It should be protected and only used when that level of administration is needed.
You can make IAM users administrators so they can still do most every admin task needed.  IAM user's access can be controlled granularly. IAM stands for Identity and Access Management and is the suite of identity services Amazon offers.
IAM users are not separate users but users that are a part of your root account.

(Tasks that require root user credentials)[https://docs.aws.amazon.com/general/latest/gr/root-vs-iam.html#aws_tasks-that-require-root]

## AWS Regions

For practice, the region closest to you is sufficient.  When selecting a region in an enterprise environment there are many factors to consider: pricing, load, compliance, latency, and services.  Some new services and features are only available in some regions.  To reduce latency or cost, the work-load can also be split across multiple regions.

## AWS CLI (command line interface) - Version 2

An open source tool that let's you interact with AWS services using commands in your terminal.  The CLI can be set up with only a little configuration.
You can also access it through CloudShell.

### Configuring the CLI

`$ aws configure`

This prompts you to enter the **aws access key**. Which are a pair (it prompts for public key first) and you can create a new pair inside the IAM console.  After their creation, when the box in the console closes the secret key cannot be viewed again.

The alias or account ID is the same for all the IAM users under your one root user's account.  The ID is a 12 digit number found inside each account.

### Commands

**Finding the Version**
    $ aws --version
    aws-cli/2.8.3 Python/3.9.11 Darwin/21.6.0 exe/x86_64 prompt/off

#### IAM

**Find out the alias to your current, working account**
    $ aws iam list-account-aliases                
    {
        "AccountAliases": [
            "root-ji"
        ]
    }

**Find out which user is signed in to CLI**
    $ aws iam get-user

#### S3 Buckets

**list all buckets**
    $ aws s3 ls

**moving, removing, and copying files**
Use --exclude or --include to filter results. Example is immediately below.

**Remove all of one type of file, or matching the provided regex pattern**
    % aws s3 rm s3://practice-bucket1-root-ji --recursive --exclude "*" --include "*.jpg"
    delete: s3://practice-bucket1-root-ji/147008004_1028711377539545_928341489216840378_n.jpg
    delete: s3://practice-bucket1-root-ji/meme-be_careful_not_todehumanize.jpg

The --exclude option has to be here or you will delete EVERYTHING.

# Redis

Redis is an In-Memory Database that provides very fast read, write, and search capabilities.  The database's information is stored inside the memory of the redis server and therefore offers much lower latency than if the data were on a disk (disk access is slow).  Multiple services can connect and utilize a Redis server simulataneously without issue.  Redis can automatically back up the data to disk if desired.  Then if the Redis server goes down, at least the data up and to that point persists.

The foundational data type of Redis are Strings.  These are stored as key, value pairs and from that basic structure, Redis implements several other datatypes.  
The types of data supported by Redis are :

- Binary-safe strings.
- Lists: collections of string elements sorted according to the order of insertion. They are basically linked lists.
- Sets: collections of unique, unsorted string elements.
- Sorted sets, similar to Sets but where every string element is associated to a floating number value, called score. The elements are always taken sorted by their score, so unlike Sets it is possible to retrieve a range of elements (for example you may ask: give me the top 10, or the bottom 10).
- Hashes, which are maps composed of fields associated with values. Both the field and the value are strings. This is very similar to Ruby or Python hashes.
- Bit arrays (or simply bitmaps): it is possible, using special commands, to handle String values like an array of bits: you can set and clear individual bits, count all the bits set to 1, find the first set or unset bit, and so forth.
- HyperLogLogs: this is a probabilistic data structure which is used in order to estimate the cardinality of a set. Don't be scared, it is simpler than it seems... - See later in the HyperLogLog section of this tutorial.
- Streams: append-only collections of map-like entries that provide an abstract log data type. They are covered in depth in the Introduction to Redis Streams.

External programs talk to Redis using a TCP socket and a Redis specific protocol. This protocol is implemented in the Redis client libraries for the different programming languages. However to make hacking with Redis simpler Redis provides a command line utility that can be used to send commands to Redis. This program is called redis-cli.

Run Redis in interactive mode:
    $ redis-cli

## Redis on Kubernetes

Create your redis config map and pod:
<https://phoenixnap.com/kb/kubernetes-redis>

If your pod is named "redis", start the redis pod with :
    kubectl exec -it redis -- redis-cli

Test it is working by sending "PING".  Should spit out "PONG" back.
Exit the Redis pod with: quit

Get info about a Redis server:
    Start redis-cli and send:
        HELLO

### Redis Commands

    To see all commands relating to the client connection
        CLIENT HELP

    Return a random key:
        RANDOMKEY
    
    Enter some basic string values:
        SET [key] [value]

    - values have to be encapsulated in quotes if there are spaces
    - you can escape values with \

## Redis Errors/Troubleshooting

**Problem:**
    [scottj@kctl-intern1 ~]$ kubectl get pods
    NAME           READY   STATUS       RESTARTS   AGE
    redis          1/1     Running      0          3d1h
    redis-client   0/1     StartError   0          3d

redis-client shows start error.

Solution: Turned out I was being an idiot and put the client configuration there on kubernetes.  We only need the server there.  Also it did not try restarting the client bc the configuration was set to "Restart: Never", presumably because it was a tutorial.

**Problem:**
Jedis was giving this error inside the debug console -
        redis.clients.jedis.exceptions.JedisConnectionException: Failed to create socket.
No values were able to be sent to Redis. The resource did not successfully connect.

Fake Solution:
    Have you checked if the port for the Redis server in kubernetes has been exposed?
    I checked with:
        kubectl get svc --all-namespaces

    It turned out, no, there was no exposed 6379 port for redis.
    
    Showing the DNS layer on kubernetes with what ports are exposed:
        kubectl get services kube-dns --namespace=kube-system

A Soulution:
    Redis did not have have a service layer in front of it.  I tried to make one and it ended up being more complicated than imagined, getting the port forwarding set up correctly.  Doable but you need extra tags and need them arranged so the service layer forwards things via its target port.  The service layer then needs to be NodePort type and have a nodePort under ports to allow outside connection.  NodePorts need to be in the 3000-3999 range.

**Problem**
VS Code tells you that you need to add the maxmemory key, value pair to your yaml.  

Solution:
Don't believe it, VS CODE LIES.  This is what happened:
[scottj@kctl-intern1 ~]$ kubectl apply -f redis-server/redis1/redis-pod.yaml
The Pod "redis1" is invalid:

- spec.containers[0].resources.limits[maxmemory]: Invalid value: "maxmemory": must be a standard resource type or fully qualified
- spec.containers[0].resources.limits[maxmemory]: Invalid value: "maxmemory": must be a standard resource for containers
- spec.containers[0].resources.requests[maxmemory]: Invalid value: "maxmemory": must be a standard resource type or fully qualified
- spec.containers[0].resources.requests[maxmemory]: Invalid value: "maxmemory": must be a standard resource for containers

### Redis Client in Quarkus

Quarkus autocreates the RedisClient if you have the dependency added to the ?? main pom.xml file and build the project, and you also have it configured in your application configuration file.  

If it does not find the client you try to use the @Inject tag to inject it, your client will be null and it will throw an exception when you try to do anything like send a command.

I am still figuring out where to put the dependency to make it work but believe it needs to be in the root pom.xml.

[Quarkus RedisClient Class File](https://github.com/quarkusio/quarkus/blob/592c48987f7c7e3f50599dfaadbcc79f4ab1425a/extensions/redis-client/runtime/src/main/java/io/quarkus/redis/client/RedisClient.java)

<https://github.com/quarkusio/quarkus/search?q=RedisClient>

<https://github.com/machi1990/quarkus/tree/d7e13b7273bf41179f410436485947f45ba59155/integration-tests/redis-client>

<https://quarkus.io/guides/redis>

### Jedis Redis Client

<https://github.com/redis/jedis>
<https://www.baeldung.com/jedis-java-redis-client-library>

<https://javapointers.com/how-to/use-redis-java-using-jedis/>

**Mocking the Jedis Connection**
At start of service inject IP address and port.  Mockito will mock the jedis connection.


# Python

## pip

Upgrade pip:
    python3 -m pip install --upgrade pip

### pip install packages

System-wide install:
    cd
    python3 -m pip install synthesizer
    
Specific and min version:
    python3 -m pip install SomePackage==1.0.4     # specific version
    python3 -m pip install 'SomePackage>=1.0.4'     # minimum version

## Stings

String slicing:
    s[start:finish] # does not include finish element

## Pep8

### Imports

Imports are usually on separate lines like so:
    `import newspaper

    from newspaper import Article
    from nltk.tokenize import sent_tokenize # absolute, thrid party import
    `

Three sections to the imports:
    1. Standard library imports
    2. Related third party imports (modules that are installed and do not belong to the the current application)
    3. Local application/library specific imports

Imports should be explicit and absolute, as in the example above.

#### Not-as-good-but-sometimes-ok Relative Imports

    `from . import ap_script
    from .sibling import example`

These are acceptable when the import will be too verbose to be explicit.

'Standard library code should avoid complex package layouts and always use absolute imports.'

#### Wildcard Imports: Stay the hell away

    `from math import *
    `
You have no idea what you've imported, and even if you do, everything in that module is now in the namespace.  You don't need that and it might confuse the python interpreter.

### String Quotes

Be consistent with your style, either using all single or double quotes for strings.  When a string contains the quote used to encase strings, use the other kind instead of backslashes.

### Whitespace

Binary operators must be surrounded by one space.  These include: (=, +=, ==, <, >, !=, +, -, in, not in, is, and, or). The exception to this is when operators of different priorities are used such as * and +.  The you might take out the space around the first priority operators like so:

    `i = i + 3
    x = x*4 + 1
    f = (a+b) * (c+d)
    `
Where should operators be placed when you have a multi-line series of items like so:
    `surplus = (income
                - taxes
                - rent
                - food
                - (yearly_ira_contribution/12)
                - bills
                + side_hustle)`

### Comments

Did you know pep8 says to use inline comments sparingly? I wonder what they consider sparing.  I love a good inline comment (when it truly adds something to context).  I think they want us to avoid all unecessary ones like those that kinda tell people how python works instead of giving the reasoning or context for the line of code.

### Documentation Strings - docstring

All public methods, modules, classes, and functions need a docustring describing what the item does.
    """Performs Fast Modular Exponentiation
    Further description if I had it to put here.
    """

One liner docstrings are okay for obvious methods.  Those are all in one line like so:
    """Place key, value pair in Redis Cache"""

These docstrings appear just after the function or class definition line.

### Naming Conventions

Names that pieces of a public API should reflect the usage, rather than the implementation.  Basically don't bog down the user for your API with unneccessary details and help them know *what* that thing does, not *how*.

Be descriptive with naming.  I was told once that truly well-named APIs and code should not need comments.

Don't use Capitalized_Words_With_Underscores. CamelCase is cool though and so is lower_case_with_underscores.  Abbreviations should be all caps like so: BSTSearch (bad example).

_single_leading_underscore prevents "from newspaper import *" from importing those items.

single_trailing_underscore_ is used to avoid conflicts with Python keywords, like String\_.

__double_leading_underscore: Allows for name mangling when naming class attributes. Read more later on this.

#### Package and Modules

Modules need short, lowercase names and can have underscores used in them to improve readiblity.  Packages/libraries on the other hand should not have underscores, only lowercase letters.

Extension modules in C or C++ should have a leading _underscore in the name.

mixedCase is okay if the file is already in mixedCase.

#### Classes

Class names should use CamelCase.  Same goes for Exception names since they are Classes.

#### Functions, Methods, & Instance Variables

Use lowercase_with_underscores and _leading_underscore for private methods and instance variables.

#### Constants

ALL_UPPERCASE_WITH_UNDERSCORES

### Function and method arguments

Always self as the first argument in an instance method ( a method that pertains to an object).  Also use cls as the first argument in class methods.

### Coding Recommendations

#### Use Def statements not lambda

    def triple(x): return 3*x

Instead of:
    triple = lambda x: 3*x

## General Python Questions

### What is the __pycache__ folder?

When your python code is run, the python interpreter compiles it first into byte code and stores it in the \_\_pycache\_\_ folder.  The code makes running your program repeatedly faster.  However, if you are in testing or developement, sometimes not cleaning the cache will lead to the interpreter not realizing the files have changed and it will run old code without you knowing.

# Java

## Static Classes

A static class can be nested inside another class.  A static class cannot be an outer class in java, however.  Static classes can be instantiated without instantiating an object of the top-level class it is nested in.  Objects of the static class can access all the static methods and variables in the non-static outer class.  They cannot however access the non-static variables and methods.  You need an outer-class object to do that.  

## POJOs

A "plain old java object", known as a pojo is a simple object class in java and it may or may not follow any standard naming conventions, access methods, or implementation styles.  The point is that it is a basic java object, plain and simple.

### A Java Bean

A JavaBean is a POJO with a strict set of rules as follows:

- Access levels – our properties are private and we expose getters and setters
- Method names – our getters and setters follow the getX and setX convention (in the case of a boolean, isX can be used for a getter)
- Default Constructor – a no-argument constructor must be present so an instance can be created without providing arguments, for example during deserialization
- Serializable – implementing the Serializable interface allows us to store the state

## Try-With-Resources

The try-with-resources statement is a try statement that creates, aka declares, one or more resources (objects that need to be closed after use).  The try-with-resources statement closes the object automatically at the end of the statement.

Any object that implements the class java.lang.AutoCloseable, which includes everthing in java.io.Closeable, can be used as a resource and these items will be closed automatically on exit of the try block.

An example could be a file.  You try to open the file to do something with it and an exception occurs.  You could create the file reader and file buffer in the try () parenthesis and it would be auto-closed if reading from the file failed.

## Project Structure

## Grokking

The code is clear enough another person can immediately understand it and reproduce it.

Most important code quality factors:
    0 The code works
    1 Readability
    2 Robust
    3 Performant

## States, Mutability, and "final"

**Minimize mutability**
Java best practice is to minimize the number of states your object and class can be in so as to minimize the number of things that can go wrong.  The more states you have possible, the more cases you have to handle.

**Reflection**
Reflection allows you to access strings at runtime without modifying code.  Reflection can be very useful in certain contexts but also makes java very dangerous so you have to be mindful and make things final so they cannot be changed through reflection.

Clean Code book
Never pass in more than 3 parameters - nit pick opinion for readability

## Exceptions

Make sure you put as much useful information as possible when throwing an exception so when you're debugging you know what you need to fix.
A service is made of projects, which are made of packages, which are made of classes. You want low coupling - a change in one place does not cause changes in other places and high cohesion - if one changes, all or most should change. Almost everything should follow the Single Responsibilty Principle (SRP). For more on cohesion and coupling: <https://stackoverflow.com/questions/14000762/what-does-low-in-coupling-and-high-in-cohesion-mean>

## ->

-> part of syntax for lambda expressions. -> separates the parameters (left-side) from the implementation (right-side).
(parameters) -> {Body}

The lambda expression is as close as we get to a function being an object in Java.  If your lambda expression takes in only one parameter, you can omit the parenthesis around the parameter.  You can also omit the braces around the body if it consists of only one expression.  It is assumed that the expression is being returned so no return keyword is needed for singular statment lambda expressions.  Here are some examples:
https://www.javatpoint.com/java-lambda-expressions

## Switch Statements

**Example**
A very beautiful switch statement: <https://github.com/bertrandmartel/speed-test-lib/blob/master/jspeedtest/src/main/java/fr/bmartel/speedtest/SpeedTestTask.java>
    final URL url = new URL(uri);

    mProtocol = url.getProtocol();

    switch (mProtocol) {
        case "http":
        case "https":
            String downloadRequest;

            if (mProxyUrl != null) {
                this.mHostname = mProxyUrl.getHost();
                this.mPort = mProxyUrl.getPort() != -1 ? mProxyUrl.getPort() : 8080;
                downloadRequest = "GET " + uri + " HTTP/1.1\r\n" + "Host: " + url.getHost() +
                        "\r\nProxy-Connection: Keep-Alive" + "\r\n\r\n";
            } else {
                this.mHostname = url.getHost();
                if (url.getProtocol().equals("http")) {
                    this.mPort = url.getPort() != -1 ? url.getPort() : 80;
                } else {
                    this.mPort = url.getPort() != -1 ? url.getPort() : 443;
                }
                downloadRequest = "GET " + uri + " HTTP/1.1\r\n" + "Host: " + url.getHost() + "\r\n\r\n";
            }
            writeDownload(downloadRequest.getBytes());
            break;
        case "ftp":
            final String userInfo = url.getUserInfo();
            String user = SpeedTestConst.FTP_DEFAULT_USER;
            String pwd = SpeedTestConst.FTP_DEFAULT_PASSWORD;

            if (userInfo != null && userInfo.indexOf(':') != -1) {
                user = userInfo.substring(0, userInfo.indexOf(':'));
                pwd = userInfo.substring(userInfo.indexOf(':') + 1);
            }
            startFtpDownload(uri, user, pwd);
            break;
        default:
            SpeedTestUtils.dispatchError(mSocketInterface, mForceCloseSocket, mListenerList,
                    SpeedTestError.UNSUPPORTED_PROTOCOL,
                    "unsupported protocol");
            break;

## Imports

Imports happen at compile time so has no bearing on runtime in Java.  The packages imported are compiled into jvm bytecodes before runtime. It's best to use specific imports rather than the regex "*" which imports everything in the declared package.  
Example of bad-practice import:
    import java.util.*;

Example of better import:
    import java.util.Map;

## Maps

java.util.* contains the map interface through which you can create 3 different types of maps: HashMap, LinkedHashMap, TreeMap. A TreeMap is a sorted map

To create a new HashMap object:
    Map<String, Integer> myMap = new HashMap<String, Integer>();

To create a new map and add multiple items at once use:
    Map<String, Integer> myMap = Map.of("juice", 500, "mashed potatoes", 600, "salad", 400);

## Strings

Java strings are immutable.  They are essentially arrays of chars.

string length:
    int len = "Hello".length();

## Files

**WOW in-depth tut that helped me with under the hood Path and File stuff:**
<https://golb.hplar.ch/2017/09/Pluggable-file-systems-in-Java.html>


### java.io.File

<https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/io/File.html>
File path names are system dependent.
The filesystem referenced when gettting a path is the path of that file within THAT system.  So with a virtual filesystem, you need to reference that and a different system if you are copying from another place?  Yes.

## Jackson API - turning objects into json strings and back

<https://www.geeksforgeeks.org/convert-java-object-to-json-string-using-jackson-api/>
    Paths.get(dir + "/abc.txt") >> is this as path in the default filesystem

    Remember the virtual filesystem lives parallel to the default filesystem. Paths have a filesystem and can not be used in an other filesystem. They are not just names.

Notes:

    Working with virtual filesystems avoid the Paths class. This class will always work in the default filesystem. Files is ok because you have create a path in the correct filesystem first.

**How can I copy a file into another location and replace it, if existing?**
    Path p2 = Paths.get("two.txt");
    Files.copy(p1, p2, StandardCopyOption.REPLACE_EXISTING);

**How do I get the current working directory?**
 String currentPath = new java.io.File(".").getCanonicalPath();
 System.out.println("Current dir:" + currentPath);

**How can I store a file in-memory?**

Use the jimfs library : <https://github.com/google/jimfs>

Maven dependency:
`<dependency>
    <groupId>com.google.jimfs</groupId>
    <artifactId>jimfs</artifactId>
    <version>1.2</version>
</dependency>`

### speed-test-lib

How the download

Download protocol for download speed test:
<https://github.com/bertrandmartel/speed-test-lib/blob/master/jspeedtest/src/main/java/fr/bmartel/speedtest/SpeedTestTask.java>

**Generate Array of Random Bytes**
byte[] bytes = new byte[20];
SecureRandom.getInstanceStrong().nextBytes(bytes);

## Java Math library

The Math library is part of the standard library for java so you do not need to import it to call the functions and objects in it.  Simply reference the function or object with Math.Name.  Example: `int circumference = 2*Math.PI*radius`.  Math is a part of java.lang.

# Maven

**Changing the version of your project, via maven command**
Change version from 2.0.0 to 2.1.0:
    mvn versions:set -DgroupId=org.apache.maven.* -DartifactId=* -DoldVersion=2.* -DnewVersion=2.1.0-SNAPSHOT
<https://www.mojohaus.org/versions-maven-plugin/examples/set.html>

## Properties

### groupId

The value used to identify all of your packages accross all projects. For me, I chose is Julia-Immer, since that is my github handle.

### artifactId

The final name of the immediate project you are bundling up.
  Final name ends up: artifactId + version + ".jar"

### package

If your current project is part of a larger package, you would use that umbrella package name here.

### version

SNAPSHOT being in the version is significant for maven, as it tells maven which jar to use when compiling and running tests.  I believe...

# Quarkus

## Quarkus Main

Quarkus automatically has a main created in the background but one can be declared to override the autogenerated one.  No "override" tag is needed or anything - you just declare it normally.

**In what directory does Quarkus run the main function?**
Regardless of where you place the main, it is run within the root directory of the project.

### @QuarusMain

It's a thing. put this annotation on your main to make quarkus find it.  It seems you still need a manifest file of some sort, but may not need the Main-Class: className , attribute insdie.  I have not confirmed that.

**Problem:  When I run the jar of my quarkus project it gives the error:: no main manifest attribute**
    [scottj@b71-int-7002 workspace]$ cd edge-bandwidth-broken-main/
    [scottj@b71-int-7002 edge-bandwidth-broken-main]$ java -jar target/edge-bandwidth-1.0-SNAPSHOT.jar
    no main manifest attribute, in target/edge-bandwidth-1.0-SNAPSHOT.jar

But I used an autogenerated maven quarkus quickstart command!!!!
**Real Solution: Turns out with quarkus you need to build a different type of jar**
Add this to your application.properties file (and make one if you do not have it already in your resources folder):
    ```#packages the app as and uber-jar so it can be run - quarkus made jars don't always run otherwise
    quarkus.package.type=uber-jar```

The following "solutions" are not needed but might have something helpful for other projects.

**Wrong Solution: make a MANIFEST.MF file and declare the Main-Class**
Things to keep in mind while handling Manifest files:
    - You should leave space between the name and value of any section in manifest file, like Version:1.1 is in valid section instead write Version: 1.1 that space between colon and 1.1 really matters a lot.
    - While specifying the main class you should not add .class extension at the end of class name. Simply specify the main class by typing:
        Main-Class: Classname

<https://www.baeldung.com/java-jar-manifest#:~:text=The%20manifest%20file%20is%20named%20MANIFEST.MF%20and%20is,execute%2C%20the%20classpath%2C%20signature%20material%20and%20much%20more>.

<https://www.geeksforgeeks.org/working-with-jar-and-manifest-files-in-java/>

**maven-jar-plugin**
To auto generate a MANIFEST.MF file during the build phase:
    You just need to add the maven-jar-plugin to the project pom.xml.
    <https://stackoverflow.com/questions/34674073/how-to-generate-manifest-mf-file-during-compile-phase>

# VS Code

## Problems

### Terminal is closing, or not starting when opened

[PowerShell Error Log](resources/VSCodePowerShellTerminalAutoCloseLog.txt)

Before VS Code said it was having trouble resolving the shell.  I commented out the lines at the beginning of the .zshrc which fetch all the functions etc.  This was based on something online but that definitely didn't fix it (and why would it).

Current .zshrc:
    #.zshrc

    # Get the aliases and functions
    #if [ -f ~/.zshrc ]; then
    #    . ~/.zshrc
    #fi

    PATH="/Applications/CMake.app/Contents/bin":"$PATH"

The installation of vscode is corrupt now.  I can't even backspace.  Matybe it will be fixed, the terminal , after reinstall.

**Solution**
Reinstalling and replacing VS Code fixed the terminal.