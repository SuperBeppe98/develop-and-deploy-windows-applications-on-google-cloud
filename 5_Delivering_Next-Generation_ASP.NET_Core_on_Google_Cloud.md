[Back to Syllabus](/README.md#course-syllabus)

## Learning Objectives
- Deploy .NET Core applications to Compute Engine, App Engine, and Google Kubernetes Engine
<br>

## Introducing .NET Core
- ASP.NET Core is a new framework for cross-platform applications
- What is.NET Core?.NET Core is Microsoft's next-generation runtime
    - Well, it offers very similar fundamental APIs to the common language runtime. It's designed from the ground up to run in today's multi-platform world
    - So as well as developing applications that will be able to run a Windows operating systems, you'll be able to take your existing C Sharp Skills to code and deploy applications on a Mac and Linux operating systems as well. Similarly, you'll find that ASP.NET Core offers a familiar environment for ASP.NET and PC developers, with the ability to run on Internet Information Services on Windows operating systems
    - However, ASP.NET Core applications will also run unchanged on low cost Linux instances that are available on Google Compute Engine, and with Microsoft's available docker based image, the.NET Core on Google Kubernetes Engine as well. We'll see details and how to do this later on in this module
    - The programming model for ASP.NET Core is exactly the same as ASP.NET MVC. Your code, model and controller classes are in C-Sharp and you view templates using the Razor syntax. Similarly, you'll find that Entity Framework Core is written with the same principles as the CLR version of Entity Framework.Taken together, this means that all of your knowledge of ASP.NET MVC and Entity Framework is directly portable to the new.NET Core Platform
    - We've mentioned that ASP.NET Core and Entity Framework Core will run on many Google Cloud compute products, including Compute Engine, Google Kubernetes Engine, and App Engine
- Let's start by looking at Compute Engine, Google's Infrastructure as a service product. The key difference between this scenario and our previous Compute Engine example is that the ASP.NET Core applications can run on Linux instances as well as Windows instances
    - First, you'll need to install.NET Core. Here's how you can do this on Debian Linux. First, we download the tarball for.NET Core from Microsoft. Then we unpackage and linkage so that we can run all the command line tools, including the.NET tool
    - Next, you can run the.NET command line tool. Simply create a new.NET Core application with the.NET new command. We've used the dash t option to specify that we want to create a web application. This will generate a skeleton ASP.NET Core application. It's the equivalent of creating a project in Visual Studio
    - Next, we run.NET restore, which as the name suggests, will perform restore operation. Restore in this context means fetch all new Git packages that are found at the project information file. When this command completes, all the.NET assemblies needed to run this application will be downloaded to our machine
    - Finally, we execute the application using.NET Run. This will start a simple web server on port 5000. We can connect to our application using curl. When we do this, the.NET Core run-time will compile our application, respond to the HTTP request, and send back an HTTP response
<br>

## ASP.NET Core and Google Kubernetes Engine 
- Google Kubernetes Engine or GA, is a hybrid service product designed to run containerized applications, will start the section by introducing docker containers and the kubernetes container orchestration system. A concise definition of what a container is, is that it provides lightweight application virtualization. We're familiar with the virtual machines, which virtualizes the computer, the operating system providing CPU, memory disk, and networking resources to the operating system.
    - A rest level virtualization is resource intensive. It will be on to advocate multiple calls, gigabytes or RAM, and disk space to run a single virtual machine. If we installed every part of our application onto a single virtual machine, we could potentially run into the problem called works on my machine, where each parts dependencies are uncontrolled. Containers are a response to the desire in modern application development, to keep each component part for the application in a controlled, and isolated environment
    - With containers, each piece of software is packaged up into a standalone image, but it's not a full operating system. Only the libraries and settings needed to ensure the application can run are included. So it's easy to ensure lightweight, self contained, and reproducible deployment for your application. The most popular software for containerization is darker, although it's not the only format.
    - Kubernetes, is an open source container orchestration system created by google, it enables you to manage containerized applications. An in depth discussion of Kubernetes is outside the scope of this class, but just be aware that you'll be able to exploit the same types of features that we've seen for creating resilient workloads on google cloud, for example, Kubernetes supports auto scaling and load balancing, using a declarative format. Google Cloud contains several resources to support containerized software
    - Firstly, GKE enables you to create a cluster to run your Kubernetes applications. Secondly, container registry gives you secure location to store your docker images, that will be deployed to the GKE cluster
    - So what does that mean for ASP.NET Core applications? Well, first we need to publish our application and we do this with the dotnet command line tools publish command. This builds an output DLA file, that's used as an entry point for our application
        - Next, we can turn our attention to packaging up our application, as a docker image. We do this by writing a Docker file, which is a specification that enables Docker to build the image. This slide shows the entire contents of the Docker file. Microsoft maintained an image for dotnet core, which we use as a starting point for ASP Core web applications. Recall that we said in a containerized environment, the image contains only the libraries and the configuration needed to run the application. So starting with the Microsoft darkness base image, we copy over the files from the publishing stock, into our new application image.
        - The next statements configure the network environment. Remember by default ASP.NET Core Applications run on Port 5000. We could configure GKE to map this port, to make it available. But later on we'll be using this Docker image on app engine. An app engine requires that our web application, should listen for requests on Port 80 80. So we exposed port 80 80 from the container, and then set the environment variable to ASP.NET Core users, to configure its protocol IP address on port
        - The final statement is the command to run when the container starts. Notice how we're running the dot net command, and providing the DLL generated from the published step, as the argument to the command. This will start the web server. Now we have our Docker file, we'll use it to build our Docker image. Remember that the Docker image, is a complete isolated application, that can be executed on a container runtime such as Dockers runtime, or google Kubernetes engine. This slide contains a complete set of commands to run on the command line to create a Docker image, store container registry, and then run the application on GKE
            - The first statement builds the Docker Image, using the Docker command line utility
            - The dash t switch provides a tag for the image, and then the format must follow the specifications on the slide with gcr.io slash the project id, slash, then your choice of application name
            - The command on the slide contains a placeholder for your project id, so you need to replace. It also, it's really easy to miss the final period, which means the current folder
            - This command is running in the folder that contains the Docker file we read previously
            - Next, we can use the gcloud Docker command, to push the image to the container registry. Again, you must use the same format string you used with the Docker build command
            - Finally, we used to Kube control command line utility, to deploy our application. There are lots of ways of doing this, and we've picked a simple one, as we only have one container to deploy to our cluster.
        - Using Kube control run, we specify our choice of application name, the image to use, making use of the format string, the image of the registry, and the port number where the application is listening for requests. A containerized application is deployed, running, and listening for requests
        - However, we need to expose the deployment to allow clients to connect to it. We do this with a final Kube control command. You can see that with Kube control exposed deployment, we can easily set up a load balancer, and it tells that requests from the clients on port 80 should be routed through the containerized application on Port 8080
<br>

## ASP.NET Core and App Engine
- In the spectrum of Google Cloud Platform compute products, Google App Engine is the platform as a service product
- Google App Engine was Google's first Cloud Platform product
    - Starting in 2008, developers could write code and run it securely and scalably on Google service
    - The original App Engine environment, now called App Engine Standard, only supports a limited number of programming languages and this does not include ASP.NET Core
    - But now, Google have created a new environment for App Engine called App Engine flexible, which allows Dockerised applications to harness the benefits of App Engine
        - Simply supply a Docker file and a simple application configuration file then publish the application
        - As a Platform-as-a-Service product, developers using App Engine don't have to concern themselves with service, instance templates, groups, load balances, or health checks, or the clusters. All of these are Google's responsibility
        - First, create an app.yaml file that describes the App Engine application, then in the command-line, use the gcloud command to deploy the application
        - Your application will be running on App Engine in just a couple of minutes 
<br>

## Hands-on Lab: Load Balance an ASP.NET Application
- Launch the Qwiklabs tool for open the Demo
    - Create and publish a simple ASP.NET Core app
    - Create app.yaml for App Engine flexible environment
    - Deploy to App Engine flexible environment
    - Deploy a new version of your service
<br>

[Go to Next Module](./5_Delivering_Next-Generation_ASP.NET_Core_on_Google_Cloud.md)
