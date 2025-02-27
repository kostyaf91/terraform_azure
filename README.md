﻿# Terraform - Azure

### This project is part of the DevOps Bootcamp by Sela.

**This terraform template creates:**
* One vnet.
* Two subnets - one public and one private, with some security.
* VM linux scale set, with auto-scaling setting.
* Public load balancer that speaks with the scale set.
* Managed postgres that speaks only to the scale set.


*Note:* It works good with multiple environments. <br>
In my case I'm using 'staging' and 'prod', there is two files with some configurations for those environments.
### To execute:
```
terraform workspace select staging
terraform plan -out staging.plan -var-file staging.tfvars
terraform apply -var-file staging.tfvars
terraform workspace select prod
terraform plan -out prod.plan -var-file prod.tfvars
terraform apply -var-file prod.tfvars
```

### For passwords, the template generates folder 'ansible' with outputs for each environment:
* \<env>_vm_pass for vmss password
* \<env>_postgres_pass for postgresql password
* \<env>_agent_ip for agent ip
* \<env>_agent_pass for master vm password
* \<env>_lb_ip for public ip of the load balancer

### For deploying the project to the environments I'm using my anisble project.

## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_azurerm"></a> [azurerm](#requirement\_azurerm) | ~> 2.65 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_random"></a> [random](#provider\_random) | 3.1.2 |

## Modules

| Name | Source | Version |
|------|--------|---------|
| <a name="module_ansible_master_vm"></a> [ansible\_master\_vm](#module\_ansible\_master\_vm) | ./modules/linux_vm | n/a |
| <a name="module_load_balancer"></a> [load\_balancer](#module\_load\_balancer) | ./modules/load_balancer | n/a |
| <a name="module_managed_postgres"></a> [managed\_postgres](#module\_managed\_postgres) | ./modules/managed_postgres | n/a |
| <a name="module_network"></a> [network](#module\_network) | ./modules/network | n/a |
| <a name="module_vmss"></a> [vmss](#module\_vmss) | ./modules/vmss | n/a |

## Resources

| Name | Type |
|------|------|
| [random_password.ansible_password](https://registry.terraform.io/providers/hashicorp/random/latest/docs/resources/password) | resource |
| [random_password.postgres_password](https://registry.terraform.io/providers/hashicorp/random/latest/docs/resources/password) | resource |
| [random_password.vm_password](https://registry.terraform.io/providers/hashicorp/random/latest/docs/resources/password) | resource |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_instance_count"></a> [instance\_count](#input\_instance\_count) | n/a | `any` | n/a     | yes |
| <a name="input_location"></a> [location](#input\_location) | n/a | `any` | n/a     | yes |
| <a name="input_tag"></a> [tag](#input\_tag) | Prefix for resources | `string` | `"kf"`  | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_ansible_master_ip"></a> [ansible\_master\_ip](#output\_ansible\_master\_ip) | n/a |
| <a name="output_ansible_pass"></a> [ansible\_pass](#output\_ansible\_pass) | n/a |
| <a name="output_lb_ip"></a> [lb\_ip](#output\_lb\_ip) | n/a |
| <a name="output_postgres_pass"></a> [postgres\_pass](#output\_postgres\_pass) | n/a |
| <a name="output_vm_pass"></a> [vm\_pass](#output\_vm\_pass) | n/a |
