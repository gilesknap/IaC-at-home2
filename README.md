# IaC-at-home2

## Intro

A second attempt at making a kubernetes cluster at home that is described in code.

The original attempt with Raspbery Pi 4s and MAAS is here https://github.com/gilesknap/IaC-at-home.

I'll be getting some new hardware for this that is better suited for this task:

- Turing Pi v2.5.2
- 4 x RK1 compute modules
- maybe some NVME storage for each module

The Turing Pi 2.5 has a BMC that can manage the compute modules so this removes the fiddly bits of the first attempt.

## Software

I'll probably stick with k3s but drop MAAS and add in:
- ansible: for provisioning from metal
- longhorn: for primary storage with redundancy idependent of the NAS
- ArgoCD: for deploying everything to the cluster?
- what else?

## Current status

Prototyping. Initial ansible now brings up a node with ubuntu. It should scale to multiple nodes or even multiple turing pis.

With that proven it may be time to buy some more hardware.
