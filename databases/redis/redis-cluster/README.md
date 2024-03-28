## Redis Cluster

An Ansible role that configure Redis in cluster mode.

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
| **redis_deploy_method** | Deploy method (docker or host) | docker |
| **redis_version** | Version, if not set - latest is used | 7.2 |
| **redis_docker_version** | Docker image tag | 7.0.11 |
| **redis_conf_file** | Path to Redis configuration file | /etc/redis/redis.conf |
| **redis_daemon** | Name of Redis daemon | redis-server |
| **redis_master_port** | #NETWORK port | 6381 |
| **redis_slave_port** | #NETWORK port | 6382 |
| **redis_bind** | #NETWORK bind | false |
| **redis_master_dir** | #SNAPSHOTTING dir | /var/lib/redis/redis-cluster-master |
| **redis_slave_dir** | #SNAPSHOTTING dir | /var/lib/redis/redis-cluster-slave |
| **redis_password** | #SECURITY requirepass | false |
| **redis_databases** | #GENERAL databases | 16 |
| **redis_master_pidfile** | #GENERAL pidfile | /var/run/redis/redis-cluster-master.pid |
| **redis_slave_pidfile** | #GENERAL pidfile | /var/run/redis/redis-cluster-slave.pid |
| **redis_loglevel** | #GENERAL loglevel | notice |
| **redis_slowlog_log_slower_than** | #SLOW_LOG slowlog-log-slower-than | 10000 |
| **redis_slowlog_max_len** | #SLOW_LOW slowlog-max-len | 128 |
| **redis_maxmemory** | #MEMORY_MANAGEMENT maxmemory | false |
| **redis_maxmemory_policy** | #MEMORY_MANAGEMENT maxmemory-policy | noeviction |
| **redis_master_logfile** | #GENERAL master logfile | /var/log/redis/redis-cluster-master.log |
| **redis_slave_logfile** | #GENERAL slave logfile | /var/log/redis/redis-cluster-slave.log |
| **redis_db_filename** | #SNAPSHOTTING dbfilename | "dump.rdb" |
| **redis_save** | #SNAPSHOTTING save | - 900 1<br>- 300 10<br>- 60 10000 |
| **redis_logfile** | #GENERAL logfile | "" |
| **redis_stop_writes_on_bgsave_error** | #SNAPSHOTTING stop-writes-on-bgsave-error | "yes" |
| **redis_rdbcompression** | #SNAPSHOTTING rdbcompression | "yes" |
| **redis_rdbchecksum** | #SNAPSHOTTING rdbchecksum | "yes" |
| **redis_appendonly** | #APPEND_ONLY_MODE appendonly | "no" |
| **redis_appendfilename** | #APPEND_ONLY_MODE appendfilename | "appendonly.aof" |
| **redis_appendfsync** | #APPEND_ONLY_MODE appendfsync | "everysec" |
| **redis_no_appendfsync_on_rewrite** | #APPEND_ONLY_MODE no-appendfsync-on-rewrite | "no" |
| **redis_auto_aof_rewrite_percentage** | #APPEND_ONLY_MODE auto-aof-rewrite-percentage | "100" |
| **redis_auto_aof_rewrite_min_size** | #APPEND_ONLY_MODE auto-aof-rewrite-min-size | "64mb" |
| **redis_notify_keyspace_events** | #EVENT_NOTIFICATION notify-keyspace-events | "" |
| **redis_client_output_buffer_limit_normal** |  #ADVANCED_CONFIG client-output-buffer-limit-normal | 0 0 0 |
| **redis_client_output_buffer_limit_slave** |  #ADVANCED_CONFIG client-output-buffer-limit-slave | 256mb 64mb 60 |
| **redis_client_output_buffer_limit_pubsub** |  #ADVANCED_CONFIG client-output-buffer-limit-pubsub | 32mb 8mb 60 |
| **redis_hz** | #ADVANCED_CONFIG hz | 10 |
| **redis_activedefrag** | #ACTIVE_DEFRAGMENTATION activedefrag | "no" |
| **redis_docker_subnet** | Docker subnet | 172.18.1.0/24 |
| **redis_docker_ip** | Docker IP | 172.18.1.2 |

## Inventory file example for cluster mode:

The first group should always be [master_servers]!

```
[master_servers]
redis1 ansible_host=192.168.252.11 ansible_ssh_port=22 ansible_become=yes ansible_become_method=sudo ansible_user=$CLOUD_SSH_USER ansible_ssh_private_key_file=$PATH_TO_PRIVATE_KEY
redis2 ansible_host=192.168.252.12 ansible_ssh_port=22 ansible_become=yes ansible_become_method=sudo ansible_user=$CLOUD_SSH_USER ansible_ssh_private_key_file=$PATH_TO_PRIVATE_KEY
redis3 ansible_host=192.168.252.13 ansible_ssh_port=22 ansible_become=yes ansible_become_method=sudo ansible_user=$CLOUD_SSH_USER ansible_ssh_private_key_file=$PATH_TO_PRIVATE_KEY

[replication_servers]
redis4 ansible_host=192.168.252.14 ansible_ssh_port=22 ansible_become=yes ansible_become_method=sudo ansible_user=$CLOUD_SSH_USER ansible_ssh_private_key_file=$PATH_TO_PRIVATE_KEY
redis5 ansible_host=192.168.252.15 ansible_ssh_port=22 ansible_become=yes ansible_become_method=sudo ansible_user=$CLOUD_SSH_USER ansible_ssh_private_key_file=$PATH_TO_PRIVATE_KEY
redis6 ansible_host=192.168.252.16 ansible_ssh_port=22 ansible_become=yes ansible_become_method=sudo ansible_user=$CLOUD_SSH_USER ansible_ssh_private_key_file=$PATH_TO_PRIVATE_KEY

```

ACL rules example:

```
redis_ACL_rules:
      - { 
          name: "user1", 
          password: ">1",
          rules: "~cached:* +get +set -del"
        }
      - { 
          name: "user2", 
          password: "",
          rules: "~cached:* +get"
        }

```
The password must start with a character ">"!
