An Ansible role that configure MariaDB in standalone mode.

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
| **mariadb_deploy_method** | Deploy method (host or docker) | docker |
| **mariadb_host_version** | MariaDB version for deploy on host (10.6, 10.11, 11.4) make sure that the repository contains the specified version | 11.4 |
| **mariadb_docker_version** | MariaDB version for deploy in docker (supported all versions from docker hub) | 10.3.32-focal |
| **mariadb_port** | MariaDB port | 3306 |
| **wsrep_port** | MariaDB wsrep port | 4567 |
| **rsync_port** | Rsync port | 4444 |
| **mariadb_bind_address** | MariaDB bind address | 0.0.0.0 |
| **mariadb_root_password** | MariaDB root password | Xs2tF2FXU9 |
| **empty_root_pass** | MariaDB disable root password (only host) | true |
| **mariadb_docker_network_name** | Docker network name | mariadb-network |
| **mariadb_docker_container_name** | Docker container name | mariadb |
| **mariadb_docker_subnet** | Docker container subnet | 172.18.4.0/24 |
| **mariadb_docker_ip** | Docker container IP | 172.18.4.2 |
| **mariadb_docker_directory_for_volumes** | Docker volumes directory | /var/apps |
| **mariadb_max_allowed_packet** | MariaDB max allowed packet | 32M |
| **mariadb_thread_stack** | MariaDB thread stack | 512K |
| **mariadb_thread_cache_size** | MariaDB thread cache size | 64 |
| **mariadb_max_connections** | MariaDB max connections | 100 |
| **mariadb_open_files_limit** | MariaDB open files limit | 8192 |
| **mariadb_sql_mode** | MariaDB sql mode | ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION |
| **mariadb_character_set_server** | MariaDB server character set | utf8mb4 |
| **mariadb_collation_server** | MariaDB server collation | utf8mb4_unicode_ci |
| **mariadb_innodb_buffer_pool_size** | MariaDB innodb buffer pool size | 2G |
| **mariadb_innodb_file_per_table** | MariaDB innodb file per table | yes |
| **mariadb_innodb_flush_log_at_trx_commit** | MariaDB innodb flush log at trx commit | no |
| **mariadb_innodb_flush_method** | MariaDB innodb flush method | no |
| **mariadb_transaction_isolation** | MariaDB transaction isolation | no |
| **new_cluster** | Galera cluster initialization | true |

## Inventory file example for standalone mode:

```
[mariadb_standalone]
mariadb ansible_host=192.168.252.1 ansible_ssh_port=22 ansible_become=yes ansible_become_method=sudo ansible_user=$CLOUD_SSH_USER ansible_ssh_private_key_file=$PATH_TO_PRIVATE_KEY

```

