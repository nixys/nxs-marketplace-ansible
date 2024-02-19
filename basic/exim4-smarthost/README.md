An Ansible role that installs Exim4 and makes initial configuration for smarthost mode

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
| **exim4_smarthost_primary_hostname** | Primary hostname | {{ domain | default(inventory_hostname) }} |
| **exim4_smarthost_qualify_domain** | Qualify domain | {{ domain | default(inventory_hostname) }} |
| **exim4_smarthost_admin_mail** | Admin mail | {{ admin_mail | default("client-tech@nixys.io") }} |
| **exim4_smarthost_local_interfaces** | Local interfaces | 127.0.0.1 : {{ ansible_default_ipv4.address }} |
| **exim4_smarthost_relay_nets** | Relay nets | 127.0.0.1 : {{ ansible_default_ipv4.address }} |
| **exim4_smarthost_block_private_networks** | Blocking private networks | yes |
| **exim4_smarthost_smtp_port** | SMTP port | 2525 |
| **exim4_smarthost_smtps_port** | SMTPS port | 4654 |
| **exim4_smarthost_smtp_submission_port** | SMTP submission port | 5875 |
| **exim4_smarthost_dkim_selector** | DKIM selector | mail |
| **exim4_smarthost_dkim_domain** | DKIM domain | {{ domain | default(inventory_hostname) }} |
| **exim4_smarthost_deploy_method** | Deploy method ['host', 'docker'] | host |
| **exim4_smarthost_docker_version** | Docker image tag | latest |
| **exim4_smarthost_docker_subnet** | Docker container subnet | 172.18.1.0/24 |
| **exim4_smarthost_docker_ip** | Docker container ip | 172.18.1.14 |
| **exim4_smarthost_docker_listen_interface** | Docker service interface to listen to | 127.0.0.1 |
| **ansible_major_version** | Major acceptable Ansible version | 2 |
| **ansible_minor_version** | Minor acceptable Ansible version | 14 |

Features:

* SPF and DKIM generation for one mail domain
* Generated entries are saved to the /root directory

## Inventory file example

```
[common]
debian        ansible_ssh_host=192.168.251.2 ansible_ssh_port=22 ansible_become=yes ansible_become_method=sudo ansible_user=$CLOUD_SSH_USER ansible_ssh_private_key_file=$PATH_TO_PRIVATE_KEY
```