# K3S Cluster Commissioning for Turing Pi with Ansible

## Description

An infrastructure as code project to commission a k3s cluster.

Supported hardware:
- One or more Turing Pi v2.5.0 boards
- With compute modules RK1 or CM4
- ANY additional Linux nodes not in a Turing Pi (OS pre-installed)

NOTE: All of the ansible playbooks after the initial flashing of the compute modules can be applied to any k3s cluster. Only the initial flashing of the compute modules is specific to the Turing Pi.

Turing Pi is a great platform for a project like this as it provides a BMC interface that allows you to remotely flash and reboot it's compute modules. See the [Turing Pi](https://turingpi.com/) website for more information.

K3S is a lightweight Kubernetes distribution that is easy to install and manage. It is a CNCF certified Kubernetes distribution that I use for all my Kubernetes projects. See the [K3S](https://k3s.io/) website for more information.

Thanks to drunkcoding.net for some great tutorials that helped with putting this together. See the [A Complete Series of Articles on Kubernetes Environment Locally](https://drunkcoding.net/posts/ks-00-series-k8s-setup-local-env-pi-cluster/)

## Features

- Automated Flashing of the compute modules with latest Ubuntu 24.04 LTS
- Move OS to NVME or other storage device
- Install of a multi-node k3s cluster
- Install services into the cluster

## Current Software

- Ubuntu 24.04 LTS
- Latest K3S
- Nginx ingress controller
- K8S Dashboard
- Prometheus and Grafana

## Planned Software

- Let's Encrypt Cert Manager
- Longhorn
- ArgoCD
- KubeVirt
- NFS PVC auto-provisioner
- anything else that is useful

## Quick start

See the [setup](docs/setup.md) to create some keypairs and access the turingpi(s).

- install podman 4.3 or higher, git and vscode
  - configure vscode to use podman for devcontainers (docker support will be added later)
- clone this repo, open in vscode and reopen in devcontainer
- cd ansible
- edit the hosts.yml file to match the turingpi's and nodes you have
- ansible-playbook pb_ALL.yml

## Some How to's

### re-flash a single node

limit hosts to the controlling turing pi and the nodes(s) to be re-flashed. Pass in the flash_force variable to force a re-flash.

```bash
ansible-playbook pb_flash_os.yml --limit turingpi,node01 -e flash_force=true
```


