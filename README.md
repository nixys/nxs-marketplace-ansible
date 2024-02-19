# nxs-marketplace-ansible

<div id="header" align="center">
  <img src="https://www.freepnglogos.com/uploads/logo-mysql-png/logo-mysql-mysql-logo-png-images-are-download-crazypng-21.png" width="100"/>
  <img src="https://cdn.iconscout.com/icon/free/png-256/free-postgresql-9-1175120.png" width="100"/>
  <img src="https://www.vectorlogo.zone/logos/php/php-vertical.svg" width="100"/>
  <img src="https://cdn.iconscout.com/icon/free/png-256/free-nginx-3628948-3030173.png?f=webp" width="100"/>
  <img src="https://www.vectorlogo.zone/logos/nodejs/nodejs-icon.svg" width="100"/>
  <img src="https://www.vectorlogo.zone/logos/java/java-icon.svg" width="100"/>
  <img src="https://www.vectorlogo.zone/logos/rabbitmq/rabbitmq-icon.svg" width="100"/>
  <img src="https://www.vectorlogo.zone/logos/elastic/elastic-icon.svg" width="100"/>
</div>

## Introduction

This repository contains [Ansible](https://www.ansible.com/) roles and playbooks for easy deployment and configures of core technologies

## Features

* Ansible roles contain a large number of variables that allow you to deploy the tool for a specific task
* Ability to choose to deploy software on the host or with docker
* Support for different software versions

## Who can use this tool

* Developers
* System administrators
* DevOps engineers
* Those who built cloud infrastructure with [nxs-marketplace-terraform](https://github.com/nixys/nxs-marketplace-terraform) and want to quickly install the services they need

## Quickstart

### Requirements
These Ansible roles have been successfully tested using the ansible-core **2.14** for the following operations systems:
- Debian **11.8/12.4**
- Ubuntu **20.04/22.04**

### Role Variables
The available variables are listed in each role's README file, along with their default values (see **defaults/main.yml**)

### Roles:

* **Basic**: roles for basic operating system and infrastructure configuration, including installing updates, configuring users, and managing basic services
* **Container Engines**: roles for installing and configuring container engines such as Docker or Podman
* **Databases**: roles to deploy and configure databases such as MySQL, PostgreSQL, MongoDB and others
* **Dev Tools**: roles related to installing and configuring development tools including compilers, programming language interpreters, development and testing environments
* **Git Platforms**: roles to deploy and configure version control systems such as GitLab or Bitbucket
* **Logging**: roles to configure centralized logging systems such as Beats, Logstash, Kibana, Fluentd
* **Mail Servers**: roles to install and configure mail servers, including mail agents, SMTP and IMAP servers
* **Message Brokers**: roles to configure and manage community brokers such as Apache Kafka, RabbitMQ
* **Monitoring**: roles for setting up monitoring systems such as Prometheus, Zabbix, Grafana
* **Network Filesystem Tools**: roles for configuring network file systems such as NFS (Network File System)
* **Other**: roles that don't fall into other categories, or provide common features and tools that may be useful in different scenarios
* **Recovery**: roles to create and configure data recovery and backup systems, including database, file system, and configuration backups
* **Search Engines**: roles to install and customize search engines such as Elasticsearch, Sphinx
* **Security**: roles to configure and secure infrastructure, including installing and configuring firewalls, threat monitoring and security updates, and integration with access control systems such as FreeIPA and Keycloak
* **Web Servers**: roles to install and configure web servers such as Apache, Nginx, etc. and integrate with reverse proxies, load balancers, and SSL certificates

### Usage:

1. Use git to clone ansible role:
```
git clone git@github.com:nixys/nxs-marketplace-ansible.git
```
2. Сreate a file **playbook.yml** in the root of the required group (using the example of the **common** role from the **basic** block):
```bash
cd ./basic
vi ./playbook.yml
```
###### Example Playbook:
```yaml
- hosts: all
  become: yes
  roles:
    - common
```
3. Сreate a file **hosts** in the root of the required group or change file **/etc/ansible/hosts**:
###### Example hosts:
```
[common]
host1            ansible_ssh_host=192.168.252.13      ansible_ssh_port=22 ansible_become=yes ansible_become_method=sudo 
host2            ansible_ssh_host=192.168.252.14      ansible_ssh_port=22 ansible_become=yes ansible_become_method=sudo
```
4. Run playbook:
```bash
ansible-playbook playbook.yml -i ./hosts
```

## Roadmap

Following roles are already in backlog for our development team and will be released soon:

**databases**
* MySQL v8.0 (Galera Cluster)
* PostgreSQL v15.5 (Stolon)

**logging**
* Vector v0.35

## Feedback

For support and feedback please contact me:
* telegram: @remelyanov95
* e-mail: r.emelyanov@nixys.io

For news and discussions subscribe the channels:
* telegram community (news): @nxs_marketplace_ansible
* telegram community (chat): @nxs_marketplace_ansible_chat


## License

nxs-marketplace-ansible is released under the [Apache License 2.0](https://github.com/nixys/nxs-marketplace-ansible/blob/main/LICENSE).
