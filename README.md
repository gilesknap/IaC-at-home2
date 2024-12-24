# IaC-at-home2

## Description

A second attempt at making a kubernetes cluster at home that is described in code.

The original attempt with Raspbery Pi 4s and MAAS is here https://github.com/gilesknap/IaC-at-home.

I'll be getting some new hardware for this that is better suited for this task:

- Turing Pi v2.5.2
- 4 x RK1 compute modules
- maybe some NVME storage for each module

The Turing Pi 2.5 has a BMC that can manage the compute modules so this removes the fiddly bits of the first attempt.

## Software

I'll initially stick with Ubuntu and k3s but drop MAAS and add in:
- ansible: for provisioning from metal up
- longhorn: for primary storage with redundancy independent of the NAS
- ArgoCD: for deploying everything to the cluster?
- perhaps switch to Talos
- what else?
  - given that I'll have a pretty serious NPU capability (24 Tops 8bit) it will be time to start playing with AI models I guess

## Current status

The current playbook will:
- use a devcontainer to create the ansible execution environment
  - no prerequisites needed on the host except podman
  - currently podman or rootless docker is required but this can be fixed
- flash Ubuntu 2024.04 to the compute modules - both rk1 and cm4
- install k3s with one control plane and multiple workers
- install the k8s dashboard
- install client tools kubectl, helm in the devcontainer
- create a script to access the k8s dashboard from the devcontainer

## Quick start

See the [setup](docs/setup.md) to create some keypairs and access the turingpi(s).

- install podman 4.3 or higher, git and vscode
  - configure vscode to use podman for devcontainers
- clone this repo
- open the repo in vscode and reopen in devcontainer
- cd ansible
- edit the hosts.yml file to match the turingpi's and nodes you have
- ansible-playbook pb_flash_all.yml

## How to's

### re-flash a single node

limit hosts to the controlling turing pi and the nodes(s) to be re-flashed. Pass in the flash_force variable to force a re-flash.

```bash
ansible-playbook pb_flash_os.yml --limit turingpi,node01 -e flash_force=true
```
