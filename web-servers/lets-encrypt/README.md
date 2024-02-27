An Ansible role that makes initial configuration for servers

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

## Role Variables

Available variables listed below, along with default values (see `defaults/main.yml`):
| Variable | Description | Default value |
| ---      | ---      | ---      |
| **lets_encrypt_acme_client** | ACME client to install (certbot|getssl|acmesh) | certbot |
| **lets_encrypt_deploy_method** | Deploy method (host or docker) | host |
| **lets_encrypt_dry_run** | Certificate issue testing (true or false) | true |
| **lets_encrypt_webroot** | Directory for domain validation | /var/www/getssl |
| **lets_encrypt_email** | Email-adress | example@nixys.io |
| **lets_encrypt_domains** | List of domains (and subdomains) for which a certificate is required | [example.com, www.example.com] |
| **lets_encrypt_auto_renew** | Adding cron for renew certificates (true or false) | true |
| **lets_encrypt_cron_hour** | A hour for cron task | 3 |
| **lets_encrypt_cron_minute** | A minute for cron task | 30 |
| **lets_encrypt_certbot_auto_renew_user** | The user under which the cron will be executed  | example.com |
| **lets_encrypt_certbot_auto_renew_options** | Options for `certbot renew` | --quiet |
| **lets_encrypt_dns_function** | DNS choise for Acme.sh. Full list - https://github.com/Neilpang/acme.sh/tree/master/dnsapi | dns_hetzner |
| **lets_encrypt_docker_version** | Docker image tag. | 2.8.0 |
| **ansible_major_version** | Ansible major version. | 2 |
| **ansible_minor_version** | Ansible minor version. | 14 |

## Inventory file example

```
[common]
debian        ansible_ssh_host=192.168.251.2 ansible_ssh_port=22 ansible_become=yes ansible_become_method=sudo ansible_user=$CLOUD_SSH_USER ansible_ssh_private_key_file=$PATH_TO_PRIVATE_KEY
```