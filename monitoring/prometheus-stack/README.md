This is an ansible role that deploys the Prometheus stack in docker containers.

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
| Variable                           | Description                                              | Default value                                |
| ---------------------------------- | -------------------------------------------------------- | -------------------------------------------- |
| **ansible_major_version**          | Ansible major version                                    | 2                                            |
| **ansible_minor_version**          | Ansible minor version                                    | 14                                           |
| **timezone**                       | Timezone configuration                                   | "Europe/Moscow"                              |
| **ps_docker_network_name**         | Name of the Docker network                               | monitoring                                   |
| **ps_docker_subnet**               | Docker network subnet                                    | 172.18.0.0/24                                |
| **prometheus_version**             | Prometheus Docker image version                          | latest                                      |
| **prometheus_docker_container_name** | Name of the Prometheus Docker container                  | prometheus                                   |
| **prometheus_docker_ip**           | IP address for the Prometheus Docker container           | 172.18.0.2                                   |
| **prometheus_port**                | Port on which Prometheus is exposed                      | 9090                                         |
| **prometheus_docker_directory_for_volumes** | Path for Prometheus Docker volumes                     | /var/apps/prometheus_stack                   |
| **grafana_version**                | Grafana Docker image version                             | latest                                       |
| **grafana_docker_container_name**  | Name of the Grafana Docker container                     | grafana                                      |
| **grafana_docker_ip**              | IP address for the Grafana Docker container              | 172.18.0.3                                   |
| **grafana_port**                   | Port on which Grafana is exposed                         | 3000                                         |
| **grafana_docker_directory_for_volumes** | Path for Grafana Docker volumes                         | /var/apps/prometheus_stack                  |
| **alertmanager_version**           | Alertmanager Docker image version                        | latest                                       |
| **alertmanager_docker_container_name** | Name of the Alertmanager Docker container              | alertmanager                                 |
| **alertmanager_docker_ip**         | IP address for the Alertmanager Docker container         | 172.18.0.4                                   |
| **alertmanager_port**              | Port on which Alertmanager is exposed                    | 9093                                         |
| **alertmanager_docker_directory_for_volumes** | Path for Alertmanager Docker volumes                   | /var/apps/prometheus_stack                   |
| **prometheus_rotate**              | Prometheus log rotation period                           | 30d                                          |
| **prometheus_scrape_interval**     | Interval for Prometheus scrapes                          | '15s'                                        |
| **prometheus_evaluation_interval** | Interval for Prometheus rule evaluations                 | '15s'                                        |
| **prometheus_scrape_timeout**      | Timeout for Prometheus scrapes                           | '10s'                                        |
| **prometheus_external_monitor_label** | External monitor label for Prometheus                    | 'default_monitor'                           |
| **prometheus_job_name**            | Prometheus job name                                      | 'node_exporter'                             |
| **prometheus_targets**             | Prometheus scrape targets                                | ['172.18.0.1:9100']                          |
| **prometheus_alertmanagers_scheme** | Scheme for Alertmanager targets                         | 'http'                                       |
| **prometheus_alertmanagers_targets** | Alertmanager targets                                    | "alertmanager:9093"                         |
| **prometheus_rule_files_path**     | Path to Prometheus rule files                            | "/etc/prometheus/rules/node-exporter.yml"   |
| **prometheus_remote_write_url**    | URL for Prometheus remote write                          | ''                                           |
| **prometheus_remote_read_url**     | URL for Prometheus remote read                           | ''                                           |
| **grafana_data_path**              | Grafana data path                                         | '/var/lib/grafana'                           |
| **grafana_logs_path**              | Grafana logs path                                         | '/var/log/grafana'                           |
| **grafana_plugins_path**           | Grafana plugins path                                      | '/var/lib/grafana/plugins'                   |
| **grafana_provisioning_path**      | Grafana provisioning path                                 | '/etc/grafana/provisioning'                  |
| **grafana_http_port**              | Grafana HTTP port                                         | 3000                                         |
| **grafana_domain**                 | Grafana domain                                            | 'localhost'                                  |
| **grafana_root_url**               | Grafana root URL                                          | '/'                                          |
| **grafana_serve_from_sub_path**    | Serve Grafana from sub-path                               | False                                        |
| **grafana_enable_gzip**            | Enable gzip compression for Grafana                       | True                                         |
| **grafana_protocol**               | Protocol for Grafana                                      | 'http'                                       |
| **grafana_cert_file**              | Certificate file for Grafana                              | ''                                           |
| **grafana_cert_key_file**          | Certificate key file for Grafana                          | ''                                           |
| **grafana_admin_user**             | Grafana admin username                                    | 'admin'                                      |
| **grafana_admin_password**         | Grafana admin password                                    | 'password!'                                  |
| **grafana_disable_gravatar**       | Disable Gravatar in Grafana                               | False                                        |
| **grafana_anonymous_enabled**      | Enable anonymous access in Grafana                        | False                                        |
| **grafana_basic_auth_enabled**     | Enable basic authentication in Grafana                    | True                                         |
| **grafana_allow_sign_up**          | Allow user sign-up in Grafana                              | True                                         |
| **grafana_auto_assign_org**        | Auto-assign user to an organization in Grafana            | True                                         |
| **grafana_smtp_enabled**           | Enable SMTP for Grafana                                    | False                                        |
| **grafana_smtp_host**              | SMTP host for Grafana                                      | 'localhost'                                  |
| **grafana_smtp_user**              | SMTP user for Grafana                                      | ''                                           |
| **grafana_smtp_password**          | SMTP password for Grafana                                  | ''                                           |
| **grafana_smtp_from_address**      | SMTP from address for Grafana                              | 'grafana@example.com'                        |
| **grafana_alerting_enabled**       | Enable alerting in Grafana                                 | True                                         |
| **grafana_default_home_dashboard_path** | Default home dashboard path in Grafana                  | ''                                           |
| **grafana_url**                    | Grafana URL for connecting to the API                     | 'http://192.168.0.3:3000'                |
| **ds_url**                          | URL for Prometheus data source in Grafana                 | 'http://prometheus:9090'                     |
| **alertmanager_group_wait**        | Group wait time in Alertmanager                           | '30s'                                        |
| **alertmanager_group_interval**     | Group interval in Alertmanager                             | '5m'                                         |
| **alertmanager_repeat_interval**    | Repeat interval in Alertmanager                            | '3h'                                         |
| **alertmanager_receiver**           | Default receiver for Alertmanager                          | 'discord'                                    |
| **alertmanager_discord_webhook_url** | Discord webhook URL for Alertmanager                       | 'https://discord.com/api/webhooks'          |
| **alertmanager_slack_api_url**       | Slack API URL for Alertmanager                              | ''                                           |
| **alertmanager_slack_channel**       | Slack channel for Alertmanager                              | ''                                           |
| **alertmanager_mm_api_url**          | Mattermost API URL for Alertmanager                          | ''                                           |
| **alertmanager_mm_channel**          | Mattermost channel for Alertmanager                         | ''                                           |

## Inventory file example

```
[prometheus-stack]
server-v1        ansible_ssh_host=192.168.251.2 ansible_ssh_port=22 ansible_become=yes ansible_become_method=sudo ansible_user=$CLOUD_SSH_USER ansible_ssh_private_key_file=$PATH_TO_PRIVATE_KEY
```