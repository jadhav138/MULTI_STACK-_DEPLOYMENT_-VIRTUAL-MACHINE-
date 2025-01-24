# MULTI_STACK-_DEPLOYMENT_-VIRTUAL-MACHINE-


This project focuses on setting up a multi-tier web application stack on a local machine. The goal is to create a controlled environment for research and development (R&D) that mimics a production setup. This allows developers to work on systems without making changes to real servers, which are often permanent and critical. By automating the setup using Infrastructure as Code (IaaC) tools, the process becomes repeatable, efficient, and error-free.


The architecture includes several key components. NGINX acts as both a web server and a load balancer. It forwards incoming user requests to the Apache Tomcat server, which hosts the Java-based web application. The MySQL server is responsible for storing data such as user credentials. To speed up data retrieval, Memcached is used for caching frequently accessed data. RabbitMQ is set up as a message broker to enable asynchronous communication between services, though it is not yet fully functional.

![image](https://github.com/user-attachments/assets/c662d38b-67d3-4769-98b8-50c941dafd3f)

To automate the deployment, we use Vagrant and Oracle VirtualBox. Vagrant is responsible for provisioning virtual machines (VMs), while VirtualBox serves as the hypervisor to run those VMs. The Vagrant file defines the configurations for the VMs, such as IP addresses and service settings. When the command vagrant up is run in Git Bash, it automatically sets up the entire stack.

The Vagrant Host Manager plugin maps hostnames to IP addresses. This ensures that services can be accessed using simple names instead of IP addresses. Configuration files for services like Tomcat and Memcached are adjusted to allow remote connections, which are needed for communication between different VMs. By default, these services only allow local connections for security reasons, but this is modified in the setup.

![image](https://github.com/user-attachments/assets/bcd6809b-6757-4d27-8e73-86d3bc2632d3)

The process flow starts with a user request. This request is routed through NGINX, which sends it to the Tomcat server. Tomcat processes the request, queries MySQL for the necessary data, and returns it to the user. If the requested data is cached in Memcached, it is served faster without querying MySQL. RabbitMQ, though not fully active, is ready to handle communication between different components in future updates.

![image](https://github.com/user-attachments/assets/8a2e9885-ebb8-46f1-aff8-fa9291103af7)


This entire setup is automated, reducing manual work and ensuring that every deployment is consistent. Changes to configuration settings, such as passwords or service configurations, are made in a single file (application.properties). This file contains all the necessary details about the VMs and services, making the system easy to manage. The automated environment is ideal for development and testing, providing a realistic simulation of a production environment.
