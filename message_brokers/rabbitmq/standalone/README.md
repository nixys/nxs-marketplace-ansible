# RabbitMQ Ansible Role

This is an Ansible role that deploys RabbitMQ in various configurations.

## Role Overview

This Ansible role deploys RabbitMQ, a high-performance messaging broker, in different configurations based on your requirements. RabbitMQ supports various deployment methods, including host and Docker.

## Supported distributions

Note (for AWS): AMIs for these images are different depending on the region, but that's okay, the images themselves are the same. To figure out which AMI you need, go to Images/AMIs and type in the name of the
* Debian [11.8, 12.4]
  * AWS:
    - debian-11-amd64-20231013-1532-a264997c-d509-4a51-8e85-c2644a3f8ba2 [ami-0197a20e1a9f83aff]
    - debian-12-amd64-20231210-1591-prod-s2fy2g55okxhk [ami-0e308c88c5d1b5022]
  * GCP:
    - Debian GNU/Linux 11 (bullseye), x86/64, amd64
    - Debian GNU/Linux 12 (bookworm), x86/64, amd64
  * YandexCloud:
    - Debian 11 [fd8lmueoqum660atdd5r]
    - Debian 12 [fd8dfiq123s8j82s85il]
  * SberCloud:
    - Debian 11 [737527dd-2182-4ba9-aad9-adbd46750c5f)]

* Ubuntu [20.04, 22.04]
  * AWS:
    - ubuntu/images/hvm-ssd/ubuntu-focal-20.04-amd64-server-20240126-aced0818-eef1-427a-9e04-8ba38bada306 [ami-0875d33dff2aae0d5]
    - ubuntu/images/hvm-ssd/ubuntu-jammy-22.04-amd64-server-20240126-47489723-7305-4e22-8b22-b0d57054f216 [ami-0b007b61391a250a1]
  * GCP:
    - Ubuntu 20.04 LTS, x86/64, amd64, focal
    - Ubuntu 22.04 LTS, x86/64, amd64, jammy
  * YandexCloud:
    - Ubuntu 20.04 [fd8bt3r9v1tq5fq7jcna]
    - Ubuntu 22.04 [fd8s78up10fbjbe5atn7]
  * SberCloud:
    - Ubuntu 20.04 [649a6095-b042-4a4c-bb37-f4670cb472a3]
    - Ubuntu 22.04 [475decdf-7455-475e-8714-fa69cd3d778a]

## Role Variables

Available variables are listed below, along with their default values:

| Variable                           | Description                                              | Default Value                                |
| ---------------------------------- | -------------------------------------------------------- | -------------------------------------------- |
| **ansible_major_version**          | Ansible major version                                    | 2                                            |
| **ansible_minor_version**          | Ansible minor version                                    | 14                                           |
| **timezone**                       | Timezone configuration                                   | "Europe/Moscow"                              |
| **deploy_method**                  | Deployment method                                        | 'docker'                                     |
| **rabbitmq_default_user**          | Default RabbitMQ user                                    | "guest"                                      |
| **rabbitmq_default_pass**          | Default RabbitMQ password                                | "guest"                                      |
| **rabbitmq_default_vhost**         | Default RabbitMQ virtual host                            | "/"                                          |
| **rabbitmq_ip**                    | RabbitMQ IP address                                      | "0.0.0.0"                                    |
| **rabbitmq_port**                  | RabbitMQ port                                            | 5672                                         |
| **loopback_users**                 | Loopback users                                           | ["guest"]                                    |
| **disk_free_limit_mem_relative**   | Disk free limit relative to memory                       | 1.0                                          |
| **hipe_compile**                   | Enable HiPE compilation                                  | false                                        |
| **vm_memory_high_watermark**       | Memory high watermark                                    | 0.4                                          |
| **connection_log_level**           | Connection log level                                     | info                                         |
| **mirroring_log_level**            | Mirroring log level                                      | info                                         |
| **cluster_partition_handling**     | Cluster partition handling mode                          | ignore                                       |
| **rabbitmq_queue_master_locator**  | Queue master locator policy                              | "min-masters"                                |
| **inet_dist_listen_min**           | Minimum port for inter-node communication                | 25672                                        |
| **inet_dist_listen_max**           | Maximum port for inter-node communication                | 25672                                        |
| **rabbitmq_image**                 | Docker image for RabbitMQ                                | "rabbitmq:latest"                            |
| **rabbitmq_container_name**        | Docker container name for RabbitMQ                       | "rabbitmq"                                   |
| **rabbitmq_ports**                 | Port mappings for Docker                                 | ["5672:5672", "15672:15672"]                 |
| **rabbitmq_config_dir**            | Configuration directory for RabbitMQ                     | "/etc/rabbitmq"                              |

## Inventory file example

```
[rabbitmq]
server-rabbitmq        ansible_ssh_host=192.168.251.2 ansible_ssh_port=22 ansible_become=yes ansible_become_method=sudo ansible_user=$CLOUD_SSH_USER ansible_ssh_private_key_file=$PATH_TO_PRIVATE_KEY
```

This role can deploy RabbitMQ either on a host system or within a Docker container based on the specified deployment method. Ensure that the necessary dependencies are installed on the target system before running this role.