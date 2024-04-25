An Ansible role that configure Percona MySQL XtraDB Cluster with deploy in Docker or on Host.

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
| **mysql_xtradb_deploy_method** | Deploy method (host or docker) | host |
| **mysql_xtradb_docker_version** | MySQL XtraDB Docker version (8.0, 5.7 ) | 5.7 |
| **mysql_xtradb_host_version** | MySQL XtraDB Host version (57, 80) | 57 |
| **mysql_xtradb_wsrep_sst_method** | Wsrep sst method (rsync_wan, mysqldump or xtrabackup) | rsync |
| **mysql_xtradb_root_password** | root password | bu6Heehae2 |
| **mysql_xtradb_user** | Xtradb user | mysql |
| **mysql_xtradb_datadir** | Xtradb datadir | /var/lib/mysql |
| **mysql_xtradb_wsrep_cluster_address** | Xtradb wsrep cluster address | gcomm://{{ groups['xtradb_nodes_group'] | map('extract', hostvars, ['ansible_' ~ mysql_xtradb_bind_interface, 'ipv4', 'address']) | join(',') }} |
| **mysql_xtradb_master_node** | Xtradb master node | {{ hostvars[ groups['xtradb_nodes_group'][0] ].ansible_default_ipv4.address }} |
| **mysql_xtradb_service** | Xtradb service | mysql |
| **mysql_xtradb_bind_interface** | Xtradb bind interface | eth0 |
| **mysql_xtradb_bind_address** | Xtradb bind address | {{ hostvars[inventory_hostname]['ansible_' + mysql_xtradb_bind_interface]['ipv4']['address'] }} |
| **mysql_xtradb_sst_user** | Xtradb sst user | sstuser |
| **mysql_xtradb_sst_password** | Xtradb sst password | sstpassword |
| **mysql_xtradb_cluster_name** | Xtradb cluster name | pxc-cluster |
| **mysql_xtradb_cluster_name** | Xtradb cluster name | pxc-cluster |
| **mysql_xtradb_binlog_format** | Xtradb binlog format | ROW |
| **mysql_xtradb_character_set_server** | Xtradb server character set | utf8 |
| **mysql_xtradb_collation_server** | Xtradb server collation | utf8_general_ci |
| **mysql_xtradb_default_storage_engine** | Xtradb default storage engine | InnoDB |
| **mysql_xtradb_innodb_autoinc_lock_mode** | Xtradb innodb autoinc lock mode | 2 |
| **mysql_xtradb_innodb_buffer_pool_instances** | Xtradb innodb buffer pool instances | 1 |
| **mysql_xtradb_innodb_buffer_pool_size** | Xtradb innodb buffer pool size | 134217728 |
| **mysql_xtradb_innodb_file_format** | Xtradb innodb file format | Barracuda |
| **mysql_xtradb_innodb_file_format_check** | Xtradb innodb file format check | on |
| **mysql_xtradb_innodb_file_per_table** | Xtradb innodb file per table | on |
| **mysql_xtradb_innodb_flush_log_at_trx_commit** | Xtradb innodb flush log at trx commit | 2 |
| **mysql_xtradb_innodb_log_buffer_size** | Xtradb innodb log buffer size | 16777216 |
| **mysql_xtradb_innodb_log_file_size** | Xtradb innodb log file size | 50331648 |
| **mysql_xtradb_innodb_strict_mode** | Xtradb innodb strict mode | on |
| **mysql_xtradb_join_buffer_size** | Xtradb join buffer size | 262144 |
| **mysql_xtradb_log_warnings** | Xtradb log warnings | 2 |
| **mysql_xtradb_long_query_time** | Xtradb long query time | 10 |
| **mysql_xtradb_max_allowed_packet** | Xtradb max allowed packet | 4194304 |
| **mysql_xtradb_max_connections** | Xtradb max connections | 4096 |
| **mysql_xtradb_max_heap_table_size** | Xtradb max heap table size | 16777216 |
| **mysql_xtradb_max_user_connections** | Xtradb max user connections | 0 |
| **mysql_xtradb_pxc_strict_mode** | Xtradb pxc strict mode | ENFORCING |
| **mysql_xtradb_query_cache_size** | Xtradb query cache size | 1048576 |
| **mysql_xtradb_read_buffer_size** | Xtradb read buffer size | 131072 |
| **mysql_xtradb_read_rnd_buffer_size** | Xtradb read rnd buffer size | 262144 |
| **mysql_xtradb_skip_name_resolve** | Xtradb skip name resolve | 1 |
| **mysql_xtradb_slow_query_log** | Xtradb slow query log | 0 |
| **mysql_xtradb_socket** | Xtradb socket | /var/run/mysqld/mysqld.sock |
| **mysql_xtradb_sort_buffer_size** | Xtradb sort buffer size | 262144 |
| **mysql_xtradb_table_definition_cache** | Xtradb table definition cache | 1400 |
| **mysql_xtradb_table_open_cache** | Xtradb table open cache | 2000 |
| **mysql_xtradb_table_open_cache_instances** | Xtradb table open cache instances | 16 |
| **mysql_xtradb_tmp_table_size** | Xtradb tmp table size | 16777216 |
| **mysql_xtradb_repo_baseurl** | Percona Repository | http://repo.percona.com/apt |
| **mysql_xtradb_wsrep_provider** | Xtradb wsrep provider | /usr/lib/libgalera_smm.so |
| **mysql_xtradb_config_file** | Xtradb config file | wsrep.cnf |
| **mysql_docker_subnet** | Docker container subnet | 172.18.4.0/24 |
| **mysql_docker_ip** | Docker container IP | 172.18.4.2 |
| **mysql_docker_container_name** | Docker container name | percona-cluster |

## Inventory file example:

```
[xtradb_nodes_group]
mysql-1 ansible_host=192.168.252.1
mysql-2 ansible_host=192.168.252.2
mysql-3 ansible_host=192.168.252.3
```
