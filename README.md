# Description
Example Azure Gateway Load Balancer Deployment with BIG-IP using Terraform. This deploys an example Provider VNET (containing the Azure GWLB sending traffic to the BIG-IPs), and an example Consumer VNET (containing an example application). 
## Diagram

![Diagram](diagram.png)

## Prerequisites

This module is supported from Terraform 0.13 version onwards.

Below templates are tested and worked in the following version 

Terraform v0.14.0

+ provider registry.terraform.io/hashicorp/azurerm v2.28.0
+ provider registry.terraform.io/hashicorp/null v2.1.2
+ provider registry.terraform.io/hashicorp/random v2.3.0
+ provider registry.terraform.io/hashicorp/template v2.1.2

  - This solution requires an Azure account that can provision objects described in the solution.
  - This solution requires you to accept any Azure Marketplace "License/Terms and Conditions" for the images used in this solution.
    - By default, this solution uses [F5 BIG-IP Virtual Edition - BEST (PAYG 25Mbps)](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/f5-networks.f5-big-ip-best?tab=PlansAndPrice)
    - Azure CLI: 
        ```bash
        az vm image terms accept --urn f5-networks:f5-big-ip-best:f5-bigip-virtual-edition-25m-best-hourly:16.0.101000
        ```
    - For more marketplace terms information, see Azure [documentation](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/cli-ps-findimage#deploy-an-image-with-marketplace-terms).

## Usage example

- Set AZURE CREDENTIALS
```bash
TBD
```

create the vars file and update it with your settings

```bash
cp tfvars.example terraform.tfvars
# MODIFY TO YOUR SETTINGS
```

run the terraform plan to deploy all of the components into your AWS account (remember that you are responsible for the cost of those components)

```bash
terraform init
terraform plan
terraform apply
```

## BIGIP configuration steps

Connect to the BIGIP using the bigipPublicIp and bigipPassword over port 8443. https://quickstart:bigipPassword@bigipPublicIp:8443

Username: quickstart

Password: bigipPassword output value

Please note it takes a few minutes for the BIGIP to complete the onboarding process, once it's done you will be able to ssh into the jumphost.

The BIGIP gets configured with a forwarding virtual server to route accept the traffic inside the GENEVE tunnel and apply relevant security controls on it.

Create your AFM policy and logging configuration


## TEST your setup:

SCP your ssh keys to the jumphost (For Testing only, don't use long lived SSH keys)

```bash
scp ~/.ssh/id_rsa ~/.ssh/id_rsa.pub ubuntu@44.230.225.53:~/.ssh/
```

using your ssh key, connect to the Internet Vpc Jumphost - internetVpcData (workspaceManagementAddress)

```bash
ssh ubuntu@x.y.z.p
```

ssh from it to one of the spoke jumphosts (get the private ip from terraform output)

monitor the traffic in AFM

## Cleanup
use the following command to destroy all of the resources

```bash
terraform destroy
```

## Providers

| Name | Version |
|------|---------|
| azure | >= X.X |
| random | n/a |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| XXXX | XXXXX | `string` | `null` | no |

## Outputs

| Name | Description |
|------|-------------|
| XXXX  | XXXX  |

## How to Contribute

Submit a pull request

# Authors
Michael O'Leary