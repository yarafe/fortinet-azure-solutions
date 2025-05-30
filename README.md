# FortiGate Terraform modules for Microsoft Azure

## Introduction

This example Terraform code demonstrates how to deploy a FortiGate NVAs within an Azure Virtual WAN (vWAN) Hub using the module available in the [modules directory](https://github.com/40net-cloud/terraform-azure-fortigate/tree/main/modules/azurevirtualwan). The objective is to simplify the deployment process for customers and provide a more efficient way to manage the deployed resources.

The outcome of this deployment is similar to deploying FortiGate NVAs via the Azure Marketplace.
For more information on deploying FortiGate NVAs in a vWAN Hub through the Azure Marketplace, refer to the official Fortinet documentation [here](https://docs.fortinet.com/document/fortigate-public-cloud/7.4.0/azure-vwan-ngfw-deployment-guide/233362/deploying-fortigate-nvas-in-a-vwan-hub).

## Deployment

### Overview

The provided Terraform code will deploy the following resources:
In the Main Resource Group:

- Virtual WAN with a Virtual Hub
- Managed Identity with Reader role assigned
- Managed Application

In the Managed Resource Group (name ends with -mrg):
- FortiGate NVAs
   Note: These NVAs are deployed as hidden resources in the Azure Portal.

### Instructions
Follow these steps to deploy:

1. Navigate to the example directory (e.g., `examples/azurevirtualwan`).
2. Review variables defined in  `examples/azurevirtualwan/variables.tf` and ensure the all default values meet your requirements. Modify them as needed.
3. Rename the file `terraform.tfvars.txt` to `terraform.tfvars`.
4. Fill in the required variables in `terraform.tfvars` file.
5. Run the following commands:

   ```sh
   terraform init
   terraform plan
   terraform apply
   ```
### Additional Configuration Scenarios

#### Scenario 1: Using an Existing Virtual WAN
Please consider the following cases:

If you have already your Virtual wan and you want to deploy Fortigate NVAs in it. please consider the following:
- Comment out or remove the Terraform code related to Virtual WAN and Virtual Hub in `examples/azurevirtualwan/main.tf`
- Provide your existing WAN details by setting the following variables: 
  vhub_id                     = ""
  vhub_virtual_router_ip1     = ""
  vhub_virtual_router_ip2     = ""
  vhub_virtual_router_asn     = ""

#### Scenario 2: Adding Spokes
If you want to add spokes, Uncomment the relevant code for spoke1 and spoke2 in `examples/azurevirtualwan/main.tf`

#### Scenario 3: Disabling Internet Inbound Access
To disable public internet access:
- Comment out or remove the elb-pip public IP resource in `examples/azurevirtualwan/main.tf` as following:
- Update the internet_inbound variable in `examples/azurevirtualwan/main.tf` as follows:
   internet_inbound = {
      enabled        = false
   }

## Support

Fortinet-provided scripts in this and other GitHub projects do not fall under the regular Fortinet technical support scope and are not supported by FortiCare Support Services.
For direct issues, please refer to the [Issues](https://github.com/40net-cloud/terraform-azure-fortigate/issues) tab of this GitHub project.

## License

[License](/../../blob/main/LICENSE) © Fortinet Technologies. All rights reserved.
