## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

Virtual Machine Diagram VMDiagram.pdf

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Ansible folder may be used to install only certain pieces of it, such as Filebeat.

Ansible ELK Playbook(https://github.com/noheenokaoi/Project1/blob/main/Ansible/install-elk.yml)

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly redundant, in addition to restricting malicious activity to the network.
- Load Balancers distributes traffic between the various servers it is connected to.  This serves as a security measure against attacks such as Denial of Service attacks.  The advantage of a jump box is that is provides a single access point into the network, which allows for easy monitoring of the network.  Jump boxes also serves as a machine to run scripts on multiple machines such as docker and ansible playbooks.


Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the event logs and system traffic.
- Filebeats monitors the changes in log files
- Metricbeats records metrics from operating systems and services running on the server.  These metrics are able to be used in other programs that help you analyze the data.

The configuration details of each machine may be found below.


| Name     | Function | IP Address    | Operating System |
|----------|----------|---------------|------------------|
| Jump Box | Gateway  | 10.0.0.4      | Linux            |
| Web 1    | Server   | 10.0.0.5      | Linux            |
| Web 2    | Server   | 10.0.0.6      | Linux            |
| Web 3    | Server   | 10.0.0.7      | Linux            |
| ELK      | Server   | 10.1.0.6      | Linux            |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 168.62.199.79

Machines within the network can only be accessed by jump box.
- The jumpbox is the machine that is allowed to acces the ELK VM.  Its IP Address is 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 168.62.199.79        |
| Web 1    | No                  | 10.0.0.5             |
| Web 2    | No                  | 10.0.0.6             |
| Web 3    | No                  | 10.0.0.7             |
| Elk VM   | No                  | 10.1.0.6


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- The benefit of using ansible to automate configuration is that ansible allows you to create and configure containers across multiple machines.
The playbook implements the following tasks:
- Install docker.io
- Install pip3
- Install python
- sysctl -w vm.max_map_count=262144
- Launch the ELK docker container


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5
- 10.0.0.6
- 10.0.0.7

We have installed the following Beats on these machines:
- Filebeats
- Metricbeats

These Beats allow us to collect the following information from each machine:
- Filebeat collects log data.
- Metricbeat collects metrics of the operating systems and services running on your machines.  

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook file to the jumpbox.
- Update the /etc/ansible/hosts file to include the targeted webserver IP addresses and webserver groups.
- Run the playbook, and navigate to the appropriate IP address to check that the installation worked as expected.

- The playbook file is filebeat-playbook.yml. It is copied to the /etc/ansible/roles/ directory.
- You need to update the /etc/ansible/hosts file to make ansible run the playbook on a specific machine. 
- In order to check that the ELK server is running, go to http://20.80.181.117:5601/app/kibana/home

