# Kubernetes Deployment with Ansible  

This Ansible playbook automates the installation and configuration of a Kubernetes cluster using **Kubeadm** and **Containerd** as the container runtime. Additionally, it includes configurations for enabling GPU support on nodes by installing the **NVIDIA Container Toolkit** and updating the node runtime to utilize the GPU.  

## Running the Playbook  

To execute the playbook, ensure you have **root** privileges. Use the following command, including the `-kK` flags to provide the necessary authentication credentials:  

```sh
ansible-playbook master.yml -kK
```

This playbook simplifies the deployment process, making it easier to set up a Kubernetes cluster with GPU support.

## Hosts

You can setup your machines in `hosts.ini`.

```ini
# The control_plane group contains the master node
[control_plane]
master ansible_host=127.0.0.2

# The workers group contains the worker nodes
[workers]
worker1 ansible_host=127.0.0.3
worker2 ansible_host=127.0.0.4

# The gpu_nodes group contains the GPU worker nodes
[gpu_nodes:children]
workers

# The kubernetes group contains all nodes in the cluster
[kubernetes:children]
control_plane
workers
```
