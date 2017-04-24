#  Ansible Docker compose based ELK setup

# Project Description

  Blogging application in Wordpress is deployed on the AWS
  cloud.For monitorting centralised logging 
  and dashboarding is implemented using the ELK (ElasticSearch, Logstash, Kibana) 
  stack. The entire infrastructure is a container based system.

Complete Installation and Configuration Management is done using Ansible.  

Note : Python should be installed on the Remote Host for the Ansible Communication as Ansible to communicate Python dependency is there.

# Goals

  1. We will use Ansible for provisioning the minimal AWS infrastructure to
     run the ELK based logging infrastructure.

  2. We will create a Docker compose based ELK setup, so that it's repeatable
     and demonstrable on a development machine.
  
  3. Then we will deploy dockerized WordPress application.

  4. Then we will setup monitorting of application, AWS resources via ELK.

  5. We will prepare an insightful dashboard to visualize logs.

  
# Specifications

  - OS: Ubuntu Server 14.04 64-bit
  - App Server: Gunicorn/Nginx
  - Python: 2.7
  - Ansible
  - Docker 1.10
  - Wordpress official Docker image (https://hub.docker.com/_/wordpress/)
  - ElasticSearch
  - Logstash
  - Kibana
  
 # Configuring EC2
 
EC2 instance is configured via Ansible playbook. It installs the docker-engine, docker-compose and other required packages.

Run the below playbook to configure the ec2 container and setup docker.
#+BEGIN_EXAMPLE
ansible-playbook configure-ec2.yml -i hosts --private-key  <path-to-keypair>
#+END_EXAMPLE

# Configuring and Installing Wordpress Application.

Application is configured via ansible playbook. Which internally uses docker-compose file. It setups the wordress application in one container and database service inside another container.

#+BEGIN_EXAMPLE
ansible-playbook -i ../hosts deploy-app.yml --private-key <keypair>
#+END_EXAMPLE

# Configuring and Installing ELK.
 
ELK stack is configured via Ansible playbook. Which internally uses docker-compose file to setup elk stack. Customized images are build from the official docker images. Then services inside the container are started.

To do the setup run ansible playbook as follows:
    #+BEGIN_EXAMPLE
    ansible-playbook -i ../hosts deploy-elk.yml --private-key <keypair>
    #+END_EXAMPLE

