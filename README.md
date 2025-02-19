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

Environment variables defined in CI/CD setup gets mapped into the build.sh script that's run inside the Packer container, and is then picked up by Packer during build.

**Packer Specific variables**

CI/CD Variable | Variable in Packer Container | Description
---------|----------|---------
 PACKER_LOG | $packer_debug | [Packer debug enabled/disabled](https://developer.hashicorp.com/packer/docs/debugging) 
 CHECKPOINT_DISABLE | 1 | [Disable Packer update check](https://developer.hashicorp.com/packer/docs/configure#checkpoint_disable)

**vSphere specific variables from CICD**

These variables are prefixed with PKR_VAR to ensure Packer picks them up

CI/CD Variable | Variable in Packer Container | Description
---------|----------|---------
 PKR_VAR_vcenter_server | $vcenter_server | VMware vCenter host name
 PKR_VAR_vcenter_user | $vcenter_user | VMware vCenter username
 PKR_VAR_vcenter_password | $vcenter_password | Password for $vcenter_user
 PKR_VAR_vcenter_cluster | $vcenter_cluster | vCenter Cluster name
 PKR_VAR_vcenter_dc_name | $vcenter_dc_name | vCenter DataCenter name
 PKR_VAR_vcenter_portgroup_name | $vcenter_portgroup_name | PortGroup Name for the template
 PKR_VAR_vcenter_datastore | $vcenter_datastore | Datastore for the template
 PKR_VAR_vcenter_folder | $vcenter_folder | vCenter folder name to store the template in
 PKR_VAR_template_name | $vcenter_template_name | Template name

**Template specific variables**

CI/CD Variable | Variable in Packer Container | Description
---------|----------|---------
 PKR_VAR_ssh_username| $ssh_username | Username for SSH connections to the template
 PKR_VAR_ssh_password_hash| $ssh_password_hash | Hashed password for the SSH user
 PKR_VAR_ssh_authorized_keys| $ssh_authorized_keys | SSH Authorized Key to add for $ssh_username
 PKR_VAR_tpl_disk_size| $tpl_disk_size | Disk size for template
 PKR_VAR_tpl_mem_size| $tpl_mem_size | Memory size for template
 PKR_VAR_tpl_cpu_num| $tpl_cpu_num | Number of vCPUs for template
 PKR_VAR_tpl_vm_disk_controller_type| $tpl_vm_disk_controller_type | Disk controller type for template