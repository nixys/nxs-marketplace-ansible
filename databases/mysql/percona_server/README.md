An Ansible role that configure Percona MySQL in standalone mode and xtrabackup utilite.

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
| **mysql_deploy_method** | Deploy method (host or docker) | docker |
| **mysql_percona_version** | MySQL version (8.0, 5.7 ) | 5.7 |
| **mysql_port** | Mysql port | 3306 |
| **mysql_bind_address** | Mysql bind address | 0.0.0.0 |
| **mysql_root_password** | Mysql root password | Xs2tF2FXU9 |
| **mysql_percona_legacy_auth_method_80** | Percona server use legacy auth method | false |
| **mysql_docker_network_name** | Docker network name | percona-network |
| **mysql_docker_container_name** | Docker container name | percona |
| **mysql_docker_subnet** | Docker container subnet | 172.18.4.0/24 |
| **mysql_docker_ip** | Docker container IP | 172.18.4.2 |
| **mysql_docker_directory_for_volumes** | Docker volumes directory | 172.18.4.2 |
| **mysql_max_allowed_packet** | Mysql max allowed packet | 32M |
| **mysql_thread_stack** | Mysql thread stack | 512K |
| **mysql_thread_cache_size** | Mysql thread cache size | 64 |
| **mysql_max_connections** | Mysql max connections | 100 |
| **mysql_open_files_limit** | Mysql open files limit | 8192 |
| **mysql_sql_mode** | Mysql sql mode | ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION |
| **mysql_character_set_server** | Mysql server character set | utf8 |
| **mysql_collation_server** | Mysql server collation | utf8_unicode_ci |
| **mysql_innodb_buffer_pool_size** | Mysql innodb buffer pool size | 2G |
| **mysql_innodb_file_per_table** | Mysql innodb file per table | yes |
| **mysql_innodb_flush_log_at_trx_commit** | Mysql innodb flush log at trx commit | no |
| **mysql_innodb_flush_method** | Mysql innodb flush method | no |
| **mysql_transaction_isolation** | Mysql transaction isolation | no |

## Inventory file example for standalone mode:

```
[percona_mysql]
mysql ansible_host=192.168.252.1 ansible_ssh_port=22 ansible_become=yes ansible_become_method=sudo ansible_user=$CLOUD_SSH_USER ansible_ssh_private_key_file=$PATH_TO_PRIVATE_KEY

```

