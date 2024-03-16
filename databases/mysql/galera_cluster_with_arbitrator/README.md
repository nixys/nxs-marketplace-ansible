An Ansible role that installs Galera Cluster for MySQL with Galera Arbitrator and makes its initial configuration

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

## Role variables

Available variables listed below, along with default values (see `defaults/main.yml`):
| Variable | Description | Default value |
| ---      | ---      | ---      |
| **debian_pre_req_packages** | Preinstall packages for Debian | ['software-properties-common', 'gpg'] |
| **ubuntu_pre_req_packages** | Preinstall packages for Ubuntu | ['software-properties-common', 'gpg'] |
| **codership_repo_keyserver** | Codership repository keyserver | keyserver.ubuntu.com |
| **codership_repo_key** | Codership repository key | 8DA84635 |
| **mysql_wsrep_version** | MySQL version | 8.0 |
| **galera_version** | Galera version | 4 |
| **empty_root_pass** | ONLY FIRST RUN: for setting root password. Set this to false after creating cluster | true |
| **mysql_root_pass** | MySQL root password | iAAJ1yaGevT2PKj |
| **mysql_sst_user** | WSREP SST user | sst_user |
| **mysql_sst_user_pass** | WSREP SST user password | dlglt9pg27WzaaU |
| **mysql_params** | MySQL configuration parametrs (under 'mysqld' block) | see 'defaults/main.yml' |
| **galera_params** | Galera configuration parametrs (under 'mysqld' block | see 'defaults/main.yml' |
| **new_cluster** | ONLY FIRST RUN: for bootstraping seed node. Set this to false after creating cluster | true |
| **cluster_name** | Galera cluster name | galera-cluster |
| **ansible_major_version** | Ansible major version. | 2 |
| **ansible_minor_version** | Ansible minor version. | 14 |

## Inventory file example

```
[galera-cluster]
galera-1        ansible_ssh_host=192.168.251.2 ansible_ssh_port=22 ansible_become=yes ansible_become_method=sudo ansible_user=$CLOUD_SSH_USER ansible_ssh_private_key_file=$PATH_TO_PRIVATE_KEY
galera-2        ansible_ssh_host=192.168.251.3 ansible_ssh_port=22 ansible_become=yes ansible_become_method=sudo ansible_user=$CLOUD_SSH_USER ansible_ssh_private_key_file=$PATH_TO_PRIVATE_KEY
[galera-arbitrator]
garb            ansible_ssh_host=192.168.251.4 ansible_ssh_port=22 ansible_become=yes ansible_become_method=sudo ansible_user=$CLOUD_SSH_USER ansible_ssh_private_key_file=$PATH_TO_PRIVATE_KEY
```