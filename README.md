## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

!(Ariel-Beer-Honigsman/Network_Diagrams/Xcorp's_Red_Team_Web_Server_and_ELK_Server.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the complete-playbook file may be used to install only certain pieces of it, such as Filebeat.

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log data and system data.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name      | Function | IP Address | Operating System |
|---------- |----------|------------|------------------|
| RedTeamVM | Gateway  | 10.0.0.4   | Linux            |
| Web1      | DVWA     | 10.0.0.5   | Linux            |
| Web2      | DVWA     | 10.0.0.6   | Linux            |
| ELKVM     | ELK      | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the RedTeamVM and ELKVM machines can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 108.170.182.170/32

ELKVM machine can only be accessed from the internet through PORT 5601 used for Kibana.

Machines within the network can only be accessed through SSH using encrypted keys present at the RedTeamVM. Machines that can be accessed thorugh SSH with encrypted key are:
- Web1
- Web2
- ELKVM

A summary of the access policies in place can be found in the table below.

| Name      | Publicly Accessible | Allowed IP Addresses                   |
|---------- |---------------------|----------------------------------------|
| RedTeamVM | Yes                 | 108.170.182.170/32                     |
| Web1      | No                  | 10.0.0.4/32                            |
| Web2      | No                  | 10.0.0.4/32                            |
| ELKVM     | Yes (for Kibana)    | 10.0.0.4/32 SSH and 108.170.182.170/32 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it is a simple way of scaling the configuration of the ELK machine.

The playbook implements the following tasks:
- Install Docker.
- Install python3-pip.
- Increase and use increased virtual memory.
- Download and Launch Docker ELK container.
- Enable Docker on reboot.

The following screenshot shows the Playbook to install and configure the ELK VM Docker with Ansible.

!(Screenshot_Project_1/install ELK VM DOcker using YAML)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5
- 10.0.0.6

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- _TODO: filebeat collects and monitors loggin data to Web1 and Web2 virtual machines, while metricbeat collects metrics from both machines mentioned. All that information is then available to be seen through Kibana.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the complete-playbook file to your Ansible container.
- Update the hosts file to include the IPs and which machine that IP has to install.
- Run the playbook, and navigate to Kibana to check that the installation worked as expected.