---

layout: post
title:  What is Docker?

---

### What is Docker?
___

Digging in directly - straight from the docs:

>Docker is the world’s leading software container platform. Developers use Docker to eliminate “works on my machine” problems when collaborating on code with co-workers. Operators use Docker to run and manage apps side-by-side in isolated containers to get better compute density. Enterprises use Docker to build agile software delivery pipelines to ship new features faster, more securely and with confidence for both Linux, Windows Server, and Linux-on-mainframe apps.

![alt](https://www.docker.com/sites/default/files/Package%20software%40x2.png)

Okay, that makes sense. But that still isn't super clear. 

What is a container? 

Why do we need Docker? 

Is it the same as Virtual Machines?

### An ELI5 version of what containers are
____

Quoting /u/Fraa_Babbit from reddit:

>Let's imagine your computer is a dining room and the food is computer resources (memory, cpu, disk space, i/o). Old operating systems served the food buffet style. ALL the food was put out and people just came in and had all they wanted. Naturally, people (programs) who came in later had less food to choose from.


>So we upgrade the operating system to include some multi-tasking rules. And we teach people (programs) how to form a line, take only one plate of food at a time, and this makes things more fair and manageable. This works so well that soon we had rules (like "please" and "thank you" and asking people to "pass" things) that enabled everyone to SIT at the table and enjoy a nice dinner together. It was great -- as long as everyone knew the rules.


>But kids don't know the rules. And often, kids can't understand the rules if you explain them. So the kids keep running into the room and grabbing whatever they want from the table, being greedy, eating from other people's plates, causing a mess and creating chaos.


>So we create a "kids table." (VMWare) This is a completely separate table where the children can sit and food is brought to them (they can't get their own). The kids are allowed to "be kids" and do what they want -- AS LONG AS THEY DON'T LEAVE THE TABLE. This keeps the adult table sane and pleasant, but someone DOES need to check in on the kids every so often. Most of the time the kids are sitting quietly, playing, doing their own thing. Sometimes, though, there's a "Lord of the Flies" situation and some cleanup is necessary.


>Docker, in this example, is for slightly older "kids." Kids who are "ready" to sit at the adult table. Docker is the equivalent of saying to a program "you can sit here but you do NOT speak unless spoken to, you sit up straight, eat slowly, no slurping, say please and thank you, do not tell that joke you know..." These limitations allow the kid to BE at the adult table, while not really being an adult. It requires a different kind of management than kids sandboxed at the kid's table. Not really less or more, just different.


>The advantage is that it's much easier to set an extra place at the table than to set up a whole other table.


>This is, more or less, the technical difference: In vmware, programs are treated like wild animals who must be put in different cages to be fed or they would fight over their food. In Docker, the programs are more like people at a restaurant, who know not to eat from their neighbor's table (or people at a thanksgiving table, who know which plate is theirs), and so are allowed to occupy the same room at meal time.



### Virtual Machines vs Containers
____

#### Tl;dr: A VM virtualises an entire system - down to the BIOS level - to create isolation. Containers are also isolated from each other but they share a kernel.

Let's say we are running several applications in different virtual machines. 
These applications are highly isolated from one another. 


These isolated applications can write to whatever files they want and be sure another application won't delete or change them.
We can install a specific version of the OS or any libraries that are needed for each isolated application. 
In most respects it is almost as if each of these applications was running on a separate physical machine.


However, there is a cost to that. 
We have to emulate a bunch of different machines. 
Each of those emulated machines has to be running its own copy of an operating system.
This is where containers have a slight advantage over VMs.

Suppose, we have a case where each application doesn't need an operating system of its own and can
work on a shared operating system. Containers are a middle ground to try to eliminate some of the cost of running multiple VMs.
While containers aren't as flexible as VMs, they still attempt to provide strong isolation between applications, but without having to run on different operating systems.


For example, they run on top of a host operating system, so there is only one instance of an operating system running on the machine. 
The tradeoff there is that you can't run a specific operating system for each of your applications. 

<img align = centre src = "https://www.sdxcentral.com/wp-content/uploads/2016/01/containers-versus-virtual-machines-docker-inc-rightscale.jpg">

### So, what is Docker?
___

Docker is a container technology that utilizes the host OS's kernel while putting the userland applications into a sandbox.
It is more lightweight than a full-fledged virtual machine, but you're applications need to be compatible with the host OS.

Docker separates the application from the infrastructure it runs on using container technology,
the same way virtual machines separate the operating systems from bare metal.

Few of the benefits of using Docker are:
* Deployment is easier.
* Docker ensures your applications and resources are isolated and segregated.
* Docker containers ensure consistency across multiple development and release cycles, standardizing your environment. 
On top of that, Docker containers work  just like git repositories, allowing you to commit changes to your Docker images and version control them. 


### Docker Components:

___

#### Core Components:

**Docker Daemon** 

It is the docker enginer which runs on the host machine. Containers are spun inside of the daemon.

**Docker Client**

It is the command line interface which is used to interact with the daemon.

If the system is a Linux environment, that's all is needed. However, if it is running on non-Linux environment, a Linux VM is created on top of the non-Linux kernel on which the containers run.

#### Workflow Components:

**Docker Image**


An image is a template that contains an environment, a base operation system, an applicatio, the stack that it runs on an all its dependencies.
One of the essential features of Docker images are that they are layered in nature.

For example, the base layer can be an operating system (eg: Ubuntu). 
On top of it, an application is created with all its dependencies are created and named v1 and this version is deployed to all servers 
Now, when we are ready to work on v2, we just add another layer on top of it named v2.

And here comes the good part - all the machines that were using v1 do not have to download the entire image again - they just download the v2 layer which they need.

**Docker Container**

This is how we run the images. We spin up a container, specify an image and we are good to go - we have an environment which might contain our app with all its dependencies set up.
Some of the common operations on the containers are - start, stop, move and delete.

**Docker Registry**

This registry is where we store our images. The images can be stored publicly or privately according to the needs.
An advantage of public images is that if we need an environment with particular dependencies, instead of setting it up from scratch,
we can make use of an existing image with our requirements.

Consider the registry to be analogous to Github which contains open source, public projects which can be used according to needs.

**Dockerfile**

Dockerfile is used to automate image construction - it contains the instructions used to build the image.


Part of the appeal of Docker is that it's very easy to create custom images using the build/Dockerfile syntax.


Eg: Suppose your image has an Ubuntu layer, then a Ruby layer, then a layer that includes your webapp. 
This can all be constructed in a Dockerfile that puts the pieces together. 
This results in an image which can be used to run containers just about anywhere: your laptop, a server in a datacenter, or on an instance in a public cloud. 
If the container runs your app successfully on your laptop, you can ship that container to a public cloud and it'll run exactly the same.

That's about it for now. For more detailed info, visit the Docker documentation [here](https://docs.docker.com/)

Source: [What is Docker?](https://www.youtube.com/watch?v=aLipr7tTuA4) and reddit. 











