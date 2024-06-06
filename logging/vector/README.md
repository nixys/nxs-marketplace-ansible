# Vector Ansible Role

This is an Ansible role that deploys Vector in various configurations.

## Role Overview

This Ansible role deploys Vector, a high-performance observability data router, in different configurations based on your requirements. Vector supports various modes, including agent, aggregator, and hybrid.

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
| **deploy_method**                  | Deployment method                                        | 'host'                                       |
| **vector_data_dir**                | Directory for Vector data                                | "/var/lib/vector"                            |
| **vector_mode**                    | Vector mode                                              | 'agent'                                      |
| **vector_api_enabled**             | Enable Vector API                                        | false                                        |
| **vector_api_address**             | Vector API address                                       | "127.0.0.1:8686"                             |
| **vector_agent_source_type**       | Source type for Vector agent                             | "demo_logs"                                  |
| **vector_agent_source_format**     | Source format for Vector agent                           | "syslog"                                     |
| **vector_agent_source_interval**   | Source interval for Vector agent                         | 1                                            |
| **vector_agent_transform_type**    | Transform type for Vector agent                          | "remap"                                      |
| **vector_agent_transform_inputs**  | Transform inputs for Vector agent                        | ['dummy_logs']                               |
| **vector_agent_transform_source**  | Transform source for Vector agent                        | ". = parse_syslog!(string!(.message))"      |
| **vector_agent_sink_type**         | Sink type for Vector agent                               | "console"                                    |
| **vector_agent_sink_inputs**       | Sink inputs for Vector agent                             | ['parse_logs']                               |
| **vector_agent_sink_encoding_codec** | Encoding codec for Vector agent sink                    | "json"                                       |
| **vector_aggregator_source_type**  | Source type for Vector aggregator                        | "stdin"                                      |
| **vector_aggregator_transform_type** | Transform type for Vector aggregator                    | "remap"                                      |
| **vector_aggregator_transform_inputs** | Transform inputs for Vector aggregator                  | ['aggregator_source']                        |
| **vector_aggregator_transform_source** | Transform source for Vector aggregator                  | ". = parse_syslog!(string!(.message))"      |
| **vector_aggregator_sink_type**    | Sink type for Vector aggregator                          | "console"                                    |
| **vector_aggregator_sink_inputs**  | Sink inputs for Vector aggregator                        | ['aggregator_transform']                     |
| **vector_aggregator_sink_encoding_codec** | Encoding codec for Vector aggregator sink            | "json"                                       |
| **vector_hybrid_source_type**      | Source type for Vector hybrid                            | "demo_logs"                                  |
| **vector_hybrid_source_format**    | Source format for Vector hybrid                          | "syslog"                                     |
| **vector_hybrid_source_interval**  | Source interval for Vector hybrid                        | 1                                            |
| **vector_hybrid_transform_type**   | Transform type for Vector hybrid                         | "remap"                                      |
| **vector_hybrid_transform_inputs** | Transform inputs for Vector hybrid                       | ['hybrid_source']                            |
| **vector_hybrid_transform_source** | Transform source for Vector hybrid                       | ". = parse_syslog!(string!(.message))"      |
| **vector_hybrid_sink_type**        | Sink type for Vector hybrid                              | "console"                                    |
| **vector_hybrid_sink_inputs**      | Sink inputs for Vector hybrid                            | ['hybrid_transform']                         |
| **vector_hybrid_sink_encoding_codec** | Encoding codec for Vector hybrid sink                  | "json"                                       |

## Inventory file example

```
[vector]
server-v1        ansible_ssh_host=192.168.251.2 ansible_ssh_port=22 ansible_become=yes ansible_become_method=sudo ansible_user=$CLOUD_SSH_USER ansible_ssh_private_key_file=$PATH_TO_PRIVATE_KEY
```
