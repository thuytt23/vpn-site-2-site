
# VPN Site to Site

![image](image/openstack.jpg)

## 1. Definition

VPC - a virtual private network is it is a network technology that allows us to set up a secure connection over a public network, for instance, the Internet.

Site-to-site VPN is a type of VPN that keeps data encrypted between two locations without needing credentials or client apps on devices using it.

## 2. Use case

There are some use cases/ purpose of a site-to-site VPN

- Allow your staff within your office to access servers hosted on the VPC cloud securely and seamlessly.

- Connect all workstations within the office network automatically.

- Each workstation will not have to establish the VPN connection individually.

- Establish remote user VPN when the staff is travelling/ woking onsite.

#  Openstack 

## Openstack components

6 core project of Openstack

- NOVA: Computing

- GLANCE: Image

- NEUTRON: Networking

- CINDER: Block Storage

- KEYSTONE: Indentity

- SWIFT: Object Storage

![image](image/openstack.jpg)


### 1. KEYSTONE: Indentity

Let's start with Keystone, the identity service, this is where you'll get authenticated and authorized within open stack.

Everyone has an identity and needs to be authenticated with one another. We're talking about end users as well as these component projects together.

The second important function of Keystone is it is where all the services get registered to as the central registration point, it provides a catalogue to services and users so they know how to reach open stack services.

### 2. GLANCE: Image

After identity, we will look at glance, glance, his image management, its stores, and retrieves virtual machine disk images, open stack compute makes use of this during instance provisioning.

When a VM starts, it must have an image behind it. We need to rebuild the images and load them into glance beforehand so that when the VM starts, it goes

out to glance and pulls a copy of the image from there, instead of you having to go through the whole installation process each time it's preinstalled for you and ready to go.

Instances need connectivity besides getting the image from Glance, a network for attaching the instance is required.

### 3. NEUTRON: Networking

Neutron is open stack networking and will create that virtual network and attach the VM to it, NEUTRON enables network connectivity as a service for other open stack services, such as Open Stack Compute
and has a pluggable architecture that supports many popular networking vendors and technologies.

It is very extensible.

Once you're authenticated and have an image and network available, Nova will step in, NOVA manages
the life cycle of compute instances in an open, static environment.

Some of its capabilities include launching, migrating, pausing, resizing and decommissioning of virtual machines.

### 4. NOVA: Computing

On-Demand NOVA is the layer on top of the hypervisor, and it is the one that coordinates all that network storage and compute resources you have in your cloud.

It coordinates them together.

Talk to the hypervisor and makes sure your virtual machines are launched.

### 5. CINDER: Block Storage

The next component, Zinder, is our volume service, Zinder provides persistent block storage to running instances.

Normally the virtual machines boot up with ephemeral volumes. That means when we terminate the VM, the data within the VMAs lost.

If you need to keep the data when it's terminated, attach a persistent block device to those VMS so that VM can write the information that needs to persist on that volume.

When the VM gets terminated, you're able to reattach that block volume device to another instance. This provides the ability to continue using the information that you have and the terminated instance.

This isn't shared storage, it's block storage, meaning there is a one to one relationship between the volume and the instance. There is a separate shared storage project called Manila, which provides shared file system for VMS.

### 6. SWIFT: Object Storage

Next, Project Swift provides object storage, SWIFT helps us store and retrieve simple objects like an MPEG four video file it uses and HTTP based API, where you pass objects and metadata with regular get input commands.

It's very basic file storage, but it can be very powerful. There are websites like Wikipedia that use object storage to run their entire system because of how

flexible, scalable and how simple it is.

### 7. DASHBOARD

The last one at the top here is the dashboard. It's based on a project called Horizon, which is more of a framework.

It provides a Web based self-service portal to interact with underlying open tech services, such as launching an instance, assigning IP addresses, configuring access controls and so on.

## OPENSTACK Architecture

This is the open psychological architecture, which has some more details around internal components and how things work and interact, the open stack project as a whole is designed to deliver a massively scalable cloud operating system.

One of the most important things about Open Stack is it is a collection of multiple software and not a big piece of monolithic software. It consists of several independent parts named the Open Stack Services. Each of the constituent services are designed to work together to provide a complete infrastructure as a service is.

Each service we are talking about is a different project designed, developed and maintained under the big open stack tent, the integration between services is facilitated through public application programming interfaces, APIs that each service offers and in turn can consume.

While these APIs allow each of the services to use another service, it also allows an implementer to switch out or change the internals of any service as long as they maintain the API. As you can see, each open stack project consists of various internal components that work together in harmony.

Let's take Nova as an example to the outside world. Nova Service is a single entity and has a separate API process.
This API process listens for API requests, free processes them and passes them on to other parts of NOVA for communication between the processes of one service and AM Cupie or Rabbitt.

MQ message broker is used, for example, after the Nova API gets a request from, let's say, neutron.

It passes this request to other NOVA components like Nova Conductor or compute through this message
to a database is essential for storing service state as well as other runtime data and configuration.

When deploying and configuring your open stack cloud, you can choose among several message broker and
database solutions such as Rabbitt, MQ, MySQL, Maria DB and SQL Lite.

Open stack projects share many common design patterns and implementation details, for example, the
Oslo project produces a set of Python libraries containing infrastructure code shared by many open stack
services.
The goal by doing this is to improve consistency, quality, stability and usability of open stack code.

Finally, users can access open stack via the Web based user interface implemented by Horizon via command
line clients, and by issuing API requests through tools like browser plug ins or Kerl for applications.

Several sticks are available.

Ultimately, all of these access methods issue rest API calls to the various open stack services.

Before going further, I would like to talk about the ways you can reach and use open stack, whether
you're an end user that needs a spin up, a VM or an administrator doing some stuff, you need to be
able to reach open stack to do some configuration, provisioning, maintenance, etc..

In total, we have three ways to use open stack.

- The horizon dashboard.

- Command line interface

- API axis

The important message from this line is all those three methods use API at the back end to fulfill your demands.


## NEUTRON NETWORK

### 1.

 And Neutron is the project under open stack tenso that provides network connectivity as a service,
for instance, is running on a hypervisor, neutron abstracts, ports, networks and subnets and make
those programmable with the help of APIs.

It also has a plug in architecture which makes it possible to integrate open source or proprietary vendor

technologies to provide additional services which are similarly abstracted.

Neutron has a modular architecture which you could deploy either in a centralized or distributed way,

depending on your needs.

The service works by allowing users to create their own virtual isolated networks and then attach interfaces

to them.

Those networks could remain isolated or could be connected to the rest of the world depending on requirements.

Connectivity between internal networks is achieved by creating virtual routers to create routes between

those virtual networks.

Even a virtual router can be connected to a public network, and a floating IP address could be allocated

to your instance to provide external access.

You have an instance that can reach and can be reached from the outside world.

The outside world could mean your Internet or the Internet.

Neutron is responsible for putting all the networking related configuration in place.

You just need to program Neutron via its API.

Before diving into the details of Neutron, let's have a look at the reasons for creating it.

Prior to Neutron Notebook Computes built, a networking component was prominently used by design.

Nobut networking has some drawbacks compared to neutron.

So the benefits we're talking here is mainly a comparison of neutron to legacy over networking.

I won't go into the details of NOVA networking and I won't provide a detailed comparison, but I want

to highlight what Neutron provides to us.

The Nova network gives you a limited set of topologies to create.

One of the motivations for creating Neutron was to enable the ability to create rich topologies, including

multi-tier networks, with a lot of features.

As an example, with Neutron, you can have overlapping IP addresses within the deployment, which is

important for most of open stack deployments.

By technology agnostic, we mean neutron enables us to have different technology options compared to

Nova with Neutron, we have the option to use land and green tunnels and not limited to using violence

or flat networks.

Only those tunneling mechanisms are important constructs for SDM in the data center, and they enable

us to use overlay networking on our physical legacy infrastructure.

Neutron has an extensible plug in architecture that doesn't limit open stack contributor's design and

deployment choices, it allows the community to innovate.

For example, if you have a good idea or technology, you could add it to Neutron with the help of the

pluggable open architecture.

This pluggable architecture in turn, lets us provide advanced services like load balancing, VPN firewall

and lots of other L for layer four to seven services with neutron.

These are the main motivations for using neutron instead of nowon networking, which historically used

to serve open static environments.

Let's talk about the base terminology and abstractions we have in neutron, the orange boxes at the

top are the VMS controlled by NOVA.

Each of the virtual servers has a virtual interface or a VIFF, and that's how the instance is plugged

in to the virtual fabric.

Essentially, those virtual interfaces are managed by NOVA.

It creates and manages the virtual interface and everything else below.

On the bottom of the slide is managed by neutron.

We have a virtual network in neutron and that's one of the core resources associated with the virtual

network.

We should have a virtual subnet, which is L3 construct, and in this case it is ten point zero point

zero point zero twenty four hour VMS and routers should have an IP from this subnet.

IPV six is a possibility as well.

Attached to that virtual network.

We have a virtual port.

It's the same as a port you can find on a physical switch.

It's what you connect the virtual interface to.

If you had a virtual cable, networks, ports and subnets are the three core resources that exist in

all neutron deployments.

Regardless of the extensions you enable from their neutron is responsible for taking apart.

The VM has its virtual interface and you plug that virtual interface into the ports and then now your

VM has connectivity.

### ARCHITECTURE

NEUTRON SERVER

API

Expose logical resource: subnets, ports

 QUEUE
 
 Enable
 
 
 PLUGIN








