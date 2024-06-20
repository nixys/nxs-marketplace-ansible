An Ansible role that configure Memcached in standalone mode.

## Supported distributions

Note (for AWS): AMIs for these images are different depending on the region, but that's okay, the images themselves are the same. To figure out which AMI you need, go to Images/AMIs and type in the name of the image. Below are examples of AMIs for the us-west-2 region

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

## Role variables

Available variables listed below, along with default values (see `defaults/main.yml`):
| Variable | Description | Default value |
| ---      | ---      | ---      |
| **ansible_major_version** | Ansible major version | 2 |
| **ansible_minor_version** | Ansible minor version | 14 |
| **memcached_deploy_method** | Deploy method (host or docker) | docker |
| **memcached_mode** | Deploy mode | standalone |
| **memcached_user** | Memcached username | memcache |
| **memcached_listen_port** | Memcached port | 11211 |
| **memcached_listen_ip** | Memcached bind address | 127.0.0.1 |
| **memcached_memory_limit** | Memcached max memory size | 64 |
| **memcached_max_connections** | Memcached number of incoming connections | 1024 |
| **memcached_conf_file** | Memcached configuration filename | /etc/memcached.conf |
| **memcached_pid_file** | Memcached PID file | /run/memcached/memcached.pid |
| **memcached_log_file** | Memcached logfile | /var/log/memcached.log |
| **memcached_service** | Memcached service path | /lib/systemd/system/memcached.service |
| **memcached_verbosity_level** | Memcached verbosity | -v |
| **memcached_daemon** | Memcached daemon | memcached.service |
| **memcached_compose_standalone** | Standalone docker-compose.yml | docker-compose-standalone.yml |
| **memcached_docker_dir** | Docker Compose directory | /var/apps/memcached |
| **memcached_docker_image** | Docker Memcached image | bitnami/memcached:1.6.28 |
| **memcached_docker_subnet** | Docker Compose subnet | 172.18.0.0/16 |
| **memcached_docker_ip** | Docker container IP-address | 172.18.0.11 |
|

## Inventory file example for standalone mode:

```
[memcached_standalone]
memcached ansible_host=192.168.252.1 ansible_ssh_port=22 ansible_become=yes ansible_become_method=sudo ansible_user=$CLOUD_SSH_USER ansible_ssh_private_key_file=$PATH_TO_PRIVATE_KEY

```

