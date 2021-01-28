# 1.	What is SAP cloud platform?
SAP Cloud Platform is a platform as a service developed by SAP SE for creating new applications or extending existing applications in a secure cloud computing environment managed by SAP. 

# 2.	What is Cloud Foundry? How to deploy app to CF?
Cloud Foundry (or CF) is a specification and set of software tools by the Cloud Foundry Foundation (and before that, the Linux foundation). It’s entirely open source, and any company or organization can use the tools or create a system that follows the CF specifications.

SAP has implemented Cloud Foundry on it’s SAP Cloud Platform, as a next-generation Platform as a Service (PaaS) development and runtime environment.


# 3.	What is docker and why we need it
Docker is a set of platform as a service (PaaS) products that use OS-level virtualization to deliver software in packages called containers. Containers are isolated from one another and bundle their own software, libraries and configuration files; they can communicate with each other through well-defined channels. All containers are run by a single operating system kernel and therefore use fewer resources than virtual machines.


# 4.	What is docker compose and why we need it
Compose is a tool for deploying multi-stage apps into docker containers.
With Compose, you use a YAML file to configure your application’s services. Then, with a single command, you create and start all the services from your configuration.

# 5. What is the difference between docker and the virtual machine?
Docker is container based technology and containers are just user space of the operating system. At the low level, a container is just a set of processes that are isolated from the rest of the system, running from a distinct image that provides all files necessary to support the processes. It is built for running applications. In Docker, the containers running share the host OS kernel.

A Virtual Machine, on the other hand, is not based on container technology. They are made up of user space plus kernel space of an operating system. Under VMs, server hardware is virtualized. Each VM has Operating system (OS) & apps. It shares hardware resource from the host.

VMs & Docker – each comes with benefits and demerits. Under a VM environment, each workload needs a complete OS. But with a container environment, multiple workloads can run with 1 OS. The bigger the OS footprint, the more environment benefits from containers. With this, it brings further benefits like Reduced IT management resources, reduced size of snapshots, quicker spinning up apps, reduced & simplified security updates, less code to transfer, migrate and upload workloads.
