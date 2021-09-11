## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

!(Diagrams/01_ELK_Stack_Deployment.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML playbook file may be used to install only certain pieces of it, such as Filebeat.

  Ansible/install-elk-playbook.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly secure, in addition to restricting access to the network.
- What aspect of security do load balancers protect? 
They protect the internal network from DDoS attacks.
- What is the advantage of a jump box?
It protects the internal network being exposed via a Public IP address. We can restrict the traffic coming in and that makes the network more secure.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system logs.
- What does Filebeat watch for?
Filebeat watch for log files at the locations specified
- What does Metricbeat record?
Metricbeat records statistics data.

The configuration details of each machine may be found below.

| Name    | Function | IP Address | Operating System |
|---------|----------|------------|------------------|
| Jumpbox | Gateway  | 10.0.0.4   | Linux            |
| Web-1   | Server   | 10.0.0.7   | Linux            |
| Web-2   | Server   | 10.0.0.8   | Linux            |
| ELK_VM  | Server   | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 211.26.246.128

Machines within the network can only be accessed by private IP.
- Which machine did you allow to access your ELK VM? 
Jump Box Provisioner
- What was its IP address? 
10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name    | Publicly Accessible | Allowed IP Addresses |
|---------|---------------------|----------------------|
| JumpBox | Yes                 | 211.26.246.128       |
| Web-1   | No                  | 10.0.0.4             |
| Web-2   | No                  | 10.0.0.4             |
| ELK_VM  | No                  | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Ansible can deploy multiple servers using a single playbook which can be automated to run every time the system boots up.

The playbook implements the following tasks:
- Install Docker
- Install Python
- Increase memory
- Download and launch a docker elk container
- Enable service docker on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

!(Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 10.0.0.7
- Web-2 10.0.0.8

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat can be used to monitor the log files at the locations specified, stores log events and sends them to Elasticsearch or Logstash for indexing. Metricbeat collects metrics from the OS on the server and sends them to Elasticsearch or Logstash.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk.yml file to /etc/ansible 
- Update the hosts file to include ELK VM IP (10.1.0.4)
- Run the playbook, and navigate to http://[your.ELK_VM.IP]:5601/app/kibana to check that the installation worked as expected.

!(Images/kibana.png)