.. _bede_facility:

The Bede Facility
=================

Bede is a new EPSRC-funded Tier 2 (regional) HPC cluster. It is currently being configured and tested and one of its first uses will be to support the hackathon. 

This system is particularly well suited to supporting:

* Jobs that require multiple GPUs and possibly multiple nodes
* Jobs that require much movement of data between CPU and GPU memory

NB the system was previously known as NICE-19.

Bede consists of 32 main GPU nodes each (IBM AC922) node has

* 2x IBM POWER9 CPUs (and two NUMA nodes), with
* 2x NVIDIA V100 GPUs per CPU
* Each CPU is connected to its two GPUs via high-bandwidth, low-latency NVLink interconnects (helps if you need to move lots of data to/from GPU memory)

A number of other nodes are available with T4 GPUs for inference tasks.

The sytem is also supported by:

* 100 Gb EDR Infiniband (high bandwith and low latency to support multi-node jobs)
* Lustre parallel file system (available over Infiniband and Ethernet network interfaces)
* The Slurm Scheduler



**Getting an Account**

Details will be released soon on how an account can be obtained for the hackathon.


