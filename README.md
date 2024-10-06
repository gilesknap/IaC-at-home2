# IaC-at-home2

## Intro

A second attempt at making a kubernetes cluster at home that is described in code.

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

I have some preliminary hardware and a README.md file!
