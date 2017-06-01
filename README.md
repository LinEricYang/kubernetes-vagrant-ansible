# Kubernetes Deployment based on Vagrant+Ansible
This project uses Vagrant and Ansible to provision a 3 nodes Kubernetes cluster
based on VirtualBox and Ubuntu 16.04 image.

### Prerequisites
You need the install following softwares.
- `Vagrant`, tested with Version 1.9.4.
- `VirtualBox`, tested with Version 5.0.36.
- `Ansbile`, tested with Version 2.3.0.0.

### Set up kubernetes cluster
Clone this repository to your working directory and change into that directory.

If you need proxy to access Internet on your environment, modify "proxy"
variable in Vagrantfile to

```
proxy = "http://proxy.example.com:port"
```

Use `vagrant up` to start VMs.

```
vagrant up
```

Those three machines:

| NAME | IP ADDRESS | ROLE |
| --- | --- | --- |
| k8s-node1 | 192.168.33.11 | Master |
| k8s-node2 | 192.168.33.12 | Worker |
| k8s-node3 | 192.168.33.13 | Worker |
