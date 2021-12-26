# First-Project
Project 1
Description of the Topology
The purpose of this network is to expose a load-balanced and monitored instance of DVW.
Load balancing ensures that the application will be highly available, in addition to restricting traffic to the network.


What aspect of security do load balancers protect?
Answer: Traffic,security, availability


What is the advantage of a jump box?
Answer: control,security,automation


Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.


What does Filebeat watch for? log files or locations that you specify,log events


What does Metricbeat record? metrics and statistics

The configuration details of each machine found below.


Jump-Box-Provisioner
Gateway
10.0.0.7 /104.43.213.197
Linux


Web1
Web Server
10.0.0.9
Linux


Web2
Web Server
10.0.0.10
Linux


ELK
ELK Server
10.1.0.5 /52.188.17.50
Linux


Load Balancer
Load Balancer
Static External IP 104.43.213.197
Linux


nathe
Access Control
External IP or PublicIP 24.220.152.158
Linux




Access Policies
The machines on the internal network are not exposed to the public Internet.
Only the ELK server machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

Workstation Public IP through TCP 22

Machines within the network can only be accessed by _____.

Jump-Box-Provisioner IP : 10.0.0.4 via SSH port 22
Workstation Public IP via port 22

A summary of the access policies in place can be found in the table below.



Name
Publicly Accessible
Allowed IP Addresses




Jump Box
No
Workstation Public IP on SSH  22


Web1
No
10.0.0.9 on SSH  22


Web2
No
10.0.0.10 on SSH  22


ELK Server
No
Workstation Public IP using TCP 22


Load balancer
No
Workstation Public IP on  HTTP 80




Elk Configuration
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

ansible lets you deploy apps quickly and easily. There is no need for writing your own code. Th use of playbooks makes updating your systems easy and effortless.

The playbook implements the following tasks:

Specify a different group of machines as well as a different remote user
  - name: Config elk VM with Docker
    hosts: elk
    remote_user: sysadmin
    become: true
    tasks:

Increase System Memory :
 - name: Use more memory
  sysctl:
    name: vm.max_map_count
    value: '262144'
    state: present
    reload: yes

Install the following services:
   `docker.io`
   `python3-pip`
   `docker`, which is the Docker Python pip module.

Launching and Exposing the container with these published ports:
 `5601:5601` 
 `9200:9200`
 `5044:5044`


The following screenshot displays the result of running docker ps after successfully configuring the ELK instance.


Target Machines & Beats
This ELK server is configured to monitor the following machines:

Web1 : 10.0.0.9
Web2 : 10.0.0.10

We have installed the following Beats on these machines:

ELK Server, Web1 and Web2
The ELK Stack Installed are: FileBeat and MetricBeat

These Beats allow us to collect the following information from each machine:

log events on filebeat
metrics and system statistics on metricbeat


Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:
SSH into the control node and follow the steps below:

Copy the [Ansible ELK Installation and VM Configuration ] and run the playbook using this command :  ansible-playbook install-elk.yml

Update the filebeat-playbook.yml file to include installer

Run the playbook using this command ansible-playbook filebeat-playbook.yml and navigate to Kibana > Logs : Add log data > System logs > 5:Module Status > Check data to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:

Which file is the playbook? Where do you copy it?
-pentest.yml for the ansible playbook
-filebeat.yml for the filebeat playbook
-metricbeat.yml for the metricbeat playbook
Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?
-edit the ansible config file with nano (nano ansible.cfg)
-Press CTRL + W (to search > enter remote_user then change remote_user = azureuser
