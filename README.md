# IaC-at-home2

## How to use

See the [setup](docs/setup.md) for more details.


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

Prototyping. Initial ansible now brings up a node with ubuntu. It should scale to multiple nodes or even multiple turing pis.

With that proven it may be time to buy some more hardware.

## Update 2021-09-26

Having a little re-think re hardware.
- I bought 2 RK1 boards and a Raspberry Pi CM4
- I have both types of board auto commissioning ubuntu with ansible nicely
- BUT
  - One of the RK1 boards seems to be inoperable
  - I've had very very slow response re that from Turing Pi
  - RK1 is stuck on Ubuntu 22.04
  - the maintainer of the RK1 ubuntu image has taken an indefinite break
- All this adds up to the usual conclusion that Raspberry Pi is the best supported SBC and nobody ever got fired for choosing it.
- BUT
  - the RK1 has some pretty cool features
  - The CM4 cannot use a NVME drive (or maybe over sata on some of the TP2.5 slots?)

For now I'm going to carry on with developing the ansible playbooks to get a (2 node) K8S cluster up and running.

Then maybe see if the CM5s can use NVME drives when they come out and if so, maybe go with those.

## Further Update

Perhaps I spoke too soon. Discord as lead me to this
- https://github.com/Joshua-Riek/ubuntu-rockchip/releases/tag/v2.4.0
- so maybe RK1 is worth some more effort

## How to launch

e.g. to re-flash all nodes

- launch the devcontainer
- ansible-playbook -i ansible/hosts.yml ansible/pb_flash_os.yml -e "reset=true" --vault-password-file=/etc/ansible/.vault_password.txt
