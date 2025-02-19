# Homelab CI/CD

Repository for hosting code used in CI/CD pipelines.

This repository is synced between my homelab GitLab installation and Github.

## Projects

### Image Brewery

[Hasicorp Packer](https://www.packer.io/) based templates for VMware vSphere. Uses [GitLab](https://about.gitlab.com/) [CI/CD](https://docs.gitlab.com/ci/) [pipelines](https://docs.gitlab.com/ci/pipelines/) and [Runners](https://docs.gitlab.com/runner/).

Packer is run in a container, and is configured with environment variables from the CI/CD Pipeline.

#### Ubuntu 24.04

Fully automated Ubuntu 24.04 templates.

###### Environment Variables

**Packer Specific variables**
```
PACKER_LOG=
CHECKPOINT_DISABLE=1
```

**vSphere specific variables from CICD**

```
PKR_VAR_vcenter_server=$vcenter_server
PKR_VAR_vcenter_password=$vcenter_password
PKR_VAR_vcenter_user=$vcenter_user
PKR_VAR_vcenter_cluster=$vcenter_cluster
PKR_VAR_vcenter_dc_name=$vcenter_dc_name
PKR_VAR_vcenter_portgroup_name=$vcenter_portgroup_name
PKR_VAR_vcenter_datastore=$vcenter_datastore
PKR_VAR_vcenter_template_name=$vcenter_template_name
PKR_VAR_vcenter_folder=$vcenter_folder
```

**Template specific variables**

```
PKR_VAR_ssh_username=$ssh_username
PKR_VAR_ssh_password=$ssh_password
PKR_VAR_ssh_password_hash=$ssh_password_hash
PKR_VAR_ssh_authorized_keys=$ssh_authorized_keys
PKR_VAR_tpl_disk_size=$tpl_disk_size
PKR_VAR_tpl_mem_size=$tpl_mem_size
PKR_VAR_tpl_vm_disk_controller_type=$tpl_vm_disk_controller_type
PKR_VAR_tpl_cpu_num=$tpl_cpu_num
```