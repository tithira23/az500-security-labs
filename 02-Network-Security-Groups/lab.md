# Lab 02 – Network Security Groups

## Objective

Implement Azure Network Security Group rules to restrict inbound management traffic to a virtual machine using the principle of least privilege.

## Scenario

A test Azure virtual machine requires secure management access. Instead of exposing RDP to the internet, access is restricted to a trusted public IP address only.

## Azure Services Used

- Azure Virtual Network
- Azure Subnet
- Azure Network Security Group
- Azure Virtual Machine
- Azure Portal

## Lab Resources

| Resource | Name |
|---|---|
| Resource Group | `rg-az500-nsg-lab` |
| Virtual Network | `vnet-az500-nsg-lab` |
| Subnet | `snet-workload` |
| Network Security Group | `nsg-az500-web-vm` |
| Virtual Machine | `vm-az500-nsg-test` |
| Region | `Australia East` |

## Steps Completed

1. Created a resource group for the NSG lab.
2. Created a virtual network and workload subnet.
3. Created a test Windows virtual machine.
4. Created a Network Security Group.
5. Associated the NSG with the workload subnet.
6. Added an inbound rule to allow RDP only from a trusted public IP address.
7. Verified that management access was restricted.
8. Reviewed the default deny inbound rule.
9. Captured evidence for configuration and validation.

## NSG Rule Implemented

| Rule Name | Direction | Source | Destination Port | Action | Priority |
|---|---|---|---|---|---|
| `Allow-RDP-From-Trusted-IP` | Inbound | Trusted Public IP `/32` | TCP/3389 | Allow | 100 |

## Evidence Captured

Screenshots are stored in the `screenshots` folder.

- `01-resource-group-created.png`
- `02-vnet-and-subnet-created.png`
- `03-vm-created.png`
- `04-nsg-created.png`
- `05-nsg-associated-to-subnet.png`
- `06-inbound-rules-configured.png`
- `07-my-public-ip-used.png`
- `08-rdp-or-ssh-access-tested.png`
- `09-deny-rule-or-default-deny-verified.png`
- `10-final-resource-overview.png`

## Security Concept

This lab demonstrates network traffic filtering using Azure Network Security Groups. The configuration reduces exposure by allowing RDP only from a trusted public IP address instead of allowing unrestricted internet access.

## Security Best Practice

Management ports such as RDP and SSH should not be exposed broadly to the internet. Access should be restricted using trusted IP addresses, Just-in-Time VM access, VPN, Azure Bastion, or other secure access methods.

## Outcome

The Network Security Group was successfully configured and associated with the workload subnet. Inbound RDP access was restricted to a trusted public IP address and default deny behaviour was verified.