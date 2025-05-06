# learn-docker

Challenges with servers
Each and every applicaition is highly dependent on the Underlying OS.
One VM cannot share the under-utilized resources with the neighbour VM's.
Configuration Management [ If app-a works on VM-a, there is no guarantee that app-a works on VM-b ]
Container : This a package with your Application + Pre-requisties + Libraries. This package is the container or our artifact. If this works on your linux machine, that should any where.

To run container, what should I install ?

1) You need to have a linux machine.
2) Install Container Run Time.  ( $ dnf install docker -y  ; this install PodMan Docker )
3) You're good to run your containers.
Container vs Docker
* Container is a package of your application.
* Docker is a container run-time to run the containers on linux machine. 
Docker is a container run time.
    Docker gives us high-level runtime as it uses CONTAINERD as its run-time.
    But PodMan uses containerd with the the same as dockr 

        $ dnf install docker       ( podMan docker ; We will be using it )
        $ dnf install docker-ce    ( Docker Runtime ; actual containerRun time from docker )
What is a container ?
    Container is a package of software that contains all the required elements to run your applicaition in any environment
What is Run Time ?
To run containers, you need to have a run time and among all, DOCKER was highly used
How to run a container ?
$ docker run containerName    ( this runs containers interactively killing your prompt )
$ docker run -d containerName ( this runs containers in the background by detaching from the terminal )
Common docker commands:
$ docker images                      ( shows the list of container images available on your system)
$ docker ps                          ( shows you the list of all the running containers on your system )
$ docker ps -a                       ( shows you the list of all the containers including the exited ) 
$ docker pull imageName              ( pulls the docker image from the image repository )
$ docker push imageName              ( pushes the docker image to the image repository )
$ docker stop                        ( To stop the container which is running ) 
$ docker exec -it containerName bash ( To enter in to the container )
$ docker run -d containerName   
$ docker run -d  -p 80:80 containerName 
How a docker container looks like ???
* docker.io/docker.io/imageName:version 
(repoName)(uesrName)

--> Examples of repoNames:  docker.io , ecr.io , gcr.io

Volume Mapping :
Mounint the local linux directory on the containers directory to achieve directory persistance
Port-Forwarding:
$ docker run -p 80:80  -d  nginx

Dynamic Porting:
docker run -P  -d httpd
Volume Mapping
docker run -v /home/verma/mysql-data:/var/lib/mysql  -e MYSQL_ROOT_PASSWORD=password -d mysql
Dockerfile reference :
https://docs.docker.com/engine/reference/builder/

ENTRYPOINT vs CMD
 The ENTRYPOINT specifies a command that will always be executed when the container starts. The CMD specifies arguments that will be fed to the ENTRYPOINT.
Both CMD and ENTRYPOINT instructions define what command gets executed when running a container. There are few rules that describe their co-operation.
Dockerfile should specify at least one of CMD or ENTRYPOINT commands.
ENTRYPOINT should be defined when using the container as an executable.
CMD should be used as a way of defining default arguments for an ENTRYPOINT command or for executing an ad-hoc command in a container.
CMD will be overridden when running the container with alternative arguments.
How to tag an imageName during build ?
docker build -t docker.io/sanraman/cart:v1 .

How to tag an existing image ?
docker tag docker.io/sanraman/cart:v1 imageID

What are few of the best practices of DOCKER IMAGING
    * Size of the Docker Image has to be as minimal as possible 
    * Securiy of the Images , it should zero to none vulnerabilites as per your organization standard

Important Point :
1) Stopping the container means KILLING the container 
2) Starting the container means CREATING a new container
What are the disadvantages of running Containers on the top of Docker Run Time ( On a linux machine )
    1) If you lose the Host Machine [ machine running the containers] , you would lose all the containers running on this host.

    2) In case if any container is killed, someone has to to come and start the application ( There is not autoScaling concept ) 

    3) If the containers in that Node experiences any resource crunch, containers goes for a restart

To mitigate all of it, we use Container Orchestrator !!!!
What is a Cloud Native Product ? Kubernetes is a Cloud Native Offeringn !!!!
    A Product which is designed keeping cloud in mind is referred as Cloud Native.
    But that does'nt mean that it's going work only on cloud.

    All the features of the Cloud Native Product can be gained only if we are on Cloud.

Kubernetes is an Open Source Container Orchestrator.
    1) Kubernetes can run both on Cloud and On-Prem  ( OpenSource )

    2) OpenShift ( RedHat ) is a Container Orchestration Platform for On-Prem

    3) On-Prem Editions For Kubernetes : Rancher, VMWare Tanzua , Openshift
Redhat ----> CNCF kubernetes  -----> OpenShift ( Pay ) 
If I want to use kubernetes what should I do ?
You can set up kubernets cluster in 2 ways : 

    1) Hardway  ( If you're on-prem )

        1) You create servers 
        2) Install container run-time on all the servers 
        3) Then install kubelet on all the servers 
        4) Install CNI Solution and install k8 and mark one of the node as Master 
    
    2) Managed Solution ( If you're cloud )

        1) All you do is use the PaS ( AWS : EKS  ,  GCP : GKE )
What all components did we learn so far in kubernetes ?
1) Master Node 
2) Worker Node 
3) Control Pane Conponents
4) Data Pane Conponents
5) Kubelet 
6) kuebctl 
7) kubeapi-server 
8) etcd 
9) scheduler 
10) Controller Manager 
When to have a cluster with multiple master vs a single master ?
In training, how to create the cluster ?
1) On Jenkins, run the TF Network Jobs ( This creates the network )
2) On your ws, clone the kubernetes repo and cd kubernetes/eks/
3) sudo make create
`https://docs.docker.com/reference/dockerfile/`
Containers are immutable :
* There is no concept of start or stop 
* Just run , means container will be created , task will be executed and container will be killed
* You cannot make changes on a container, even if you make you'd lose them and you have to make the changes on the image
Containers are not like OS , they are mean to run a single process

Here storage is LVM :

Expanding the disk ( like adding more disk pyhsucally on cloud , cannot be seen by the OS )
You need to run growfs to let the OS know about this space addition
Once you get the space, add this space to the Logical Volume
Then expand the fileSystem
CMD and ENTRYPOINT are a kind of startup for container

1) You can have n number of CMD, but only the latest will be considered in the Dockerfile
2) CMD is typically used to pass the arguments ( that means values mentioned in CMD can be overridden )
3) ENTRYPOINT : This also serves the same but cannot be overriden 

  $ ls -ltr 
In docker, if you mention any process by in a JSON format, it will be a process of it's own where the parent process id rectly 1 whcih is the system process.