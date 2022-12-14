[Back to Syllabus](/README.md#course-syllabus)

## Learning Objectives
- Configure Microsoft Windows and Microsoft SQL Server in Compute Engine
<br>

## Compute Engine Fundamentals 
- Compute engine is the infrastructure as a service product on Google Cloud

- When you get started with compute engine, you'll notice how easy it is to provision a virtual machine with the perfect configuration to suit your needs
- You'll be able to select up to 64 virtual CPUs per machine with between .9 and 6.5 GB of memory per CPU
- You have the choice of standard and SSD persistent disks and local SSDs
- You'll be able to get open running quickly with available Windows Server images and Linux images
    - You might be surprised to see Linux images in a class about running Windows workloads and Google Cloud but later on, you'll see how you can take your existing C sharp and dot net skills and apply them to code applications that run on Linux
    
- Here is how you create a compute engine virtual machine with the Cloud Console, web browser user interface
    - You should enter a suitable name for the VM and set the appropriate zone, which will determine the Google data center where the machine will be created
    - You can also see the machine type. This shows to virtual CPUs and 7.5 GB of memory. And a 50 gigabyte boot disk with the Windows Server 2016 image

- There are lots of other configuration options, but this shows all the basic choices that you'll need to make
    - Once your machines are configured, you'll connect them to each other using Google's virtual private cloud network resource
    - You'll automatically benefit from Google's extremely high performance network. Meaning that you'll get two gigabits per second of bandwidth per core between machines running in the same zone, with an upper limit of 16 gigabits per second of bandwidth
    - In addition, when you provision resources in different Google regions, traffic between them will flow exclusively over Google's own fiber network. Resulting in lower latency and higher throughput than if the traffic was routed through the public internet

- To protect virtual machines there is a powerful flexible yet simple to configure firewall
    - You'll be able to make your Google resources available as a seamless extension of your on premises environment using Google's virtual private network


- Finally, we'll see later that Google's infrastructure will enable you to run your application, high availability and scalability taken care of with a http and https load bouncer or a TCP and UDP load bouncer
    - At the time this video is recorded, Google's Windows Server images included Windows Server 2012 R2, 2016 and 2019
    - All with both Desktop and Core versions available as well as 20h2 Core version
    - The price for the virtual machines provisioned on Google compute engine includes the Windows Server license
    - This costs four cents per core per hour. And it's pro rated permanent with a minimum of ten minutes. Just like compute engine zone hardware building
    
- Next, let's look at Microsoft Sequel Server support. Google supplies pre configured compute engine images for express, web, standard, and enterprise editions
    - With 2012, 2014, and 2019 versions available for all except express
    - Each Sequel server edition can be deployed in a variety of versions of Windows Server
    - Once again, the default price includes both the Microsoft Windows Server and Sequel Server license cost. With the same permanent building
    - However, in this case, you'll be able to bring your own license. If you need a pre configured Windows infrastructure that's ready to go, then you want to look at Google Client Marketplace

- This example shows the ASP.NET framework solution that comes preinstalled with internet information services and ASP.NET
There is also a highly available Sequel Server solution which will install multiple servers and configure the network to enable Sequel Server always on availability groups

- Once your virtual machines are up and running, you want to connect to them to perform general systems operation tasks such as installing and configuring Windows features and your own applications
    - You'll be able to connect using remote desktop protocol and you can even do this without leaving your browser
    - Of course, you can also use Microsoft RDP clients instead

- It's common to configure your Google compute engine Windows virtual machines using startup scripts
    - Startup scripts can either run once on first boot, in system preparation or on every boot and they can be written as batch command or powershell scripts
<br>

## Architecting Windows Solutions on Compute Engine
- For traditional Windows applications, you'll want to ensure that your Windows active directory environment is extended into Google Cloud
    - You might run a read only Active Directory secondary server or perhaps use Active Directory federation services
    - You'll notice in this diagram, that we've connected the on premises resources to google cloud using the google VPN resource. This will enable you to treat the google cloud resources as a seamless extension of your private network applications and services

- Here are some useful tips in terms of Compute Engine network configuration specifically for Windows Virtual Machines
    - When you provision Virtual Machines, the default network configuration is to have a private IP address visible to the instance and a public IP address that's maintained by Compute Engine
    - When a machine doesn't have a public IP address that is not able to connect to the internet without configuring a separate machine as a network address, to translation gateway
    - This is important for Windows Virtual Machines, as they need to be able to connect to the internet to contact the Windows license server when the machine is first provisioned and subsequently at regular intervals
    - So you'll need to ensure that your network configuration supports this. It's also important to remember that there are two firewalls in play with Windows Virtual Machines, both the one running on your Windows server and Compute Engines firewall
    - The Compute Engine default firewall allows RDP traffic and iCMP so you can pin your instance. SSH is also important, but not so important for Windows VMs. You probably want to lock down RDP axis
    - So it's only possible from your own premises environment, and if you've got a VPN connection, remove the default RDP rule altogether. You'll also need to think about what other ports should be opened
    
- One final network feature is that VMs can be configured with a fixed internal IP address
    - Doing this means that the address is preserved even when the machine is shut down for an extended period of time then restarted
    - Without a fixed internal address, the address is assigned by Google's DHCP service

- Let's look at Compute Engine storage configuration
    - The default storage configuration for Windows Virtual Machines is a single 50 gigabyte persistent disk based on spinning hard drives
    - Persistent Disks on Compute Engine, our network attached block storage devices where performance scales with the size of the disks and are automatically replicated three times
    - They come in two types, Regular and SSD
    - SSD drives offer higher throughput and much higher IOPS performance than regular hard drives at a higher per gigabyte cost
    - You can have a maximum of 64 terabytes of storage per Virtual Machine and you can split this up over multiple distinct discs of different types 

- One nice feature of Compute Engine disks is that they can be attached to multiple machines in read only mode
    - In addition, you can also provision local SSDs
    - This has even higher IOPS performance than a persistent SSD but does not survive a Virtual Machine shutdown
    - You should use this as a local scratch disk or cash drive where the application needs that
    - Disks can also be backed up using Compute Engine snapshots. These integrate with the Windows volume Shadow copy service, which means that there's usually no need to pause disk activity to back up to disk and Compute Engine
    
- Another product on Google Cloud that you should be aware of is Google Cloud's operations
    - This provides single pane of glass monitoring, logging, tracing and arrow reporting across all your Compute Engine Virtual Machines
    - There is an available cloud monitoring agent for Windows to enable collection of key metrics from your Windows Virtual Machines
<br>

## High-Availability SQL Server on Compute Engine
- Let's finish off this module by looking at an example of creating complex Windows Infrastructure on Google Cloud Platform
    - Typically setting up an environment with highly available SQL Server deployments on-premises would start with a purchase order and take many weeks to complete. On GCP, you'll be able to harness a Cloud Launcher solution
    - With just a few clicks, you'll provision the entire end to end configuration
    - Mission-critical SQL Server workloads require support for high availability and disaster recovery
    - To achieve this, Google Cloud Platform supports Windows Server Failover Clustering, WSFC

- SQL Server always on availability groups
    - Always on availability groups is SQL Service flagship high availability disaster recovery solution, allowing me to configure replicas for automatic failover in the case of failure
        - These replicas can be readable, allowing you to offload read workloads and backups
        - Compute Engine users can now configure always on availability groups
        - This includes configuring replicas on virtual machines in different isolated zones, as described in this reference architecture
    - In this reference architecture, you'll need two custom subnetworks each will hold a SQL Server instance
        - We also need an Active Directory, as with most typical Windows workloads will promote this domain controller to also be the DNS server. Most SQL Server nodes need to join the Active Directory and update their own DNS settings
        - When you build the WSFC and availability group using these two nodes. Since we're using static IP addresses, the system will ask you to specify cluster IP and listener IP addresses. We need to configure these using Google Compute Engine's advanced routing, so the packet can be forwarded to the appropriate node
        - This configuration offers regional high availability. While you could create two subnetworks in the same zone, this won't handle zone level failure
        - You need two or more custom networks because the system is built on multi-site failover clustering - It also means that SQL clients need to support multi subnet failover for the optimal failure time
    - When Google have tested this, it can usually complete failover within 15 seconds. When it comes to IP addresses, cloud networking is very different from the on-premises network environments you're used to
        - At a high level, Google Compute Engine networking is like a big layer 3 switch, DHCP, and similar everyday features work differently from how you might expect based on your on-premise networking experience
        - Google Compute Engine networking doesn't know about cluster virtual IP addresses, such as the SQL Server availability group listener. It won't automatically assign a new IP address to the VM
        - As we configured Compute Engine advanced routing, the list that IP address must by definition be outside of any Google Compute Engine network address range
        - However, from the perspective of Windows running inside the VM, it has to be in the same subnet ranges the primary internal IP for the virtual machine
    - Here's a typical network configuration that Google recommends for use in this scenario
        - There are two subnets; 10.1.0.0/24 and 10.2.0.0/24. On the virtual machine's side, the VM network configuration has a subnet mask is 255.255.0.0
        - The virtual machine view of the network is a superset of the Google Compute Engine subnetwork view
        - When we pick up the listener IP address, we just need to pick up an address, which is outside of the Compute Engine subnetwork but inside the virtual machines subnet mask
    - Look at listeners IP address one as an example
        This is 10.1.1.5, which is outside of the Google Compute Engine subnet, but it's the same network as the internal IP address, 10.1.0.4 from the virtual machine perspective
<br>

## Hands-on Lab: Create a highly available SQL Server backend using AlwaysOn Availability Groups
- Launch the Qwiklabs tool for open the Demo
    - Browse the pre-created lab environment
    - Configure the failover cluster manager
    - Create an availability group
    - Test the failover
<br>

[Go to Next Module](./3_Developing_ASP.NET_MVC_applications.md)
