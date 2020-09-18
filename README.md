# Elk Stack Project
This Document Contains Following Details:
1. Network Diagram
2. Description of the Topology
3. Access Policies
4. Elk Configuration: Beats in Use/Machines Being Monitored
5. How to Use the Ansible Build

# 1. Network Diagram

![alt text](https://github.com/natereem24/UCI-ELK/blob/master/Project%2013%20diagram.PNG)
These files have been tested and used to generate a live Elk deployment on Azure. They can be used to recreate the entire deployment pictured above. Alternatively, select portions of the [filebeat-playbook.yml](https://github.com/natereem24/UCI-ELK/blob/master/filebeat-playbook.yml) file may be used to install only certain pieces of it, such as Filebeat

# 2. Description of the Topology
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application. By creating one virtual machine entitled, “jumpbox,” the containers in other vm’s can be easily modified.

Load Balancing will ensure the application is highly available, in addition to restricting unwanted traffic to the network, a prime example being a DDOS attack. By distributing the HTTP traffic between webservers, the webservers and the network will not be busy by an enormous amount of user requests; making load balancers so crucial in the industry of cybersecurity, as they not only help various applications run smoothly, but also prevent cyber attacks. 

Integrating an elk server allows users to easily monitor the vulnerable VM’s for changes to the file system and machine metrics such as uptime and cpu usage. Applications, such as the Filebeat, webservers and the DVWA application can be easily monitored for further analysis.

The Metricbeat collects metrics from the operating system in use and from services running on the server, in this case the Elk Server. 

The configuration details for each machine may be found below. 
|  Name   	   | Function  	     | IP Address    | Operating System  	|
|Jump Box      |Gateway	         |10.10.0.11	   |      Linux	        |
|Red Team VM1  | DVWA Server     |10.10.0.12   	 |   	  Linux         |
|Load Balancer | Balances Traffic|40.125.126.131 |   	  Linux         |
| Elk Server VM| Elk Server   	 |10.0.0.4   	   |   	  Linux         |

# 3. Access Policies
The machines on the internal network are not exposed to the public network. Our webservers can only be accessed through the public IP address of our load balancer.

The webserver and Elk Server can be accessed from the Jump Box Virtual Machine via port 22 and SSH keys, though, on occasion, creating an inbound rule in the Security Group settings is required. 

Only the load balancer and jump box virtual machine can accept connections from the internet. Access to this machine is only allowed from the following IP addresses:
40.125.126.131
10.10.0.12

The summary of the access policies in place can be found in the table below.
|Name   	    |IP Address   	| Publicly Accessible  	|
|Jump Box	    |	10.10.0.11    |	     Yes              |
|Red Team VM1 | 10.10.0.12  	|   	 No               |
|Load Balancer| 40.125.126.131|      Yes	            |
|Elk Server VM| 10.0.0.4  	  |   	 No               |

# 4. Elk Configuration
Ansible was used to automate configuration of the Elk machine. No configuration was performed manually, which is advantageous because human error risk is significantly reduced if done manually instead for each container or machine. It should be noted that the syntax or commands within configuration files and playbooks may need to be changed to better suit particular virtual machines. 

The install-elk.yml playbook implements the following tasks:
1. Installs docker.io-References the the IP address listed under elk in ansible’s hosts file to install docker on the target VM.
2. Increases Virtual Memory-A standard container does not have enough virtual memory to run an Elk container.
3. Installs python3-The docker module uses python.
4. Installs docker module.
5. Downloads and launches web container-Downloads and launches the Elk container, and lists the specific ports needed to access the container or application you are trying to reach.
# Target Machines & Beats
The Elk server is configured to monitor the following machines:
Red Team VM1 10.10.0.12

We have installed the following beats on these machines:

Machines:

Jump Box,
Elk,
Red Team VM1

Beats:
[filebeat-config.yml](https://github.com/natereem24/UCI-ELK/blob/master/filebeat-config.yml),
[filebeat-playbook.yml](https://github.com/natereem24/UCI-ELK/blob/master/filebeat-playbook.yml)

These beats allow us to collect the following information from each machine:
•	The filebeat elasticach module usually deals with audit logs, depreciation logs, gc logs, server logs, and slow logs.
•	The metricbeat module collects info such as cpu usage, memory, disk, network, and other varying options of a system. 
