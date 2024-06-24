# find-next-cidr
## Overview
Adding a rule to allow the Azure DevOps Build Agent VMs access to one of our public facing function apps. Being denied will cause the terraform self-service modules to stop working and delay migration.

## Description of Service
The function app (fa-uks-web-cidr-01) is hosted in our new Azure landing zone (its-appservices-01 subscription). It is used by our IAC (infrastructure as code) platform (Terraform) for creating new subnets.

There is no built-in tool in Terraform to identify the next available space to create subnets in Azure virtual networks. This function app provides this missing functionality by returning the next available subnet range for a given CIDR (Classless Inter-Domain Routing) range.

The function app is sent:
- Subscription ID
- Virtual Network Name
- Resource Group Name
- CIDR Range

And returns:
- Virtual Network Name
- Virtual Network ID
- Virtual Network Type
- Virtual Network Location
- Next Available subnet range

## Security Measures
The function app (fa-uks-web-cidr-01) uses a consumption plan that only charges cost on usage. Due to this the function app cannot use private endpoints as only premium function apps currently supports this.

Instead, the function app is locked down using IP restrictions set to the outbound IP addresses of the new landing zone firewall. Meaning that only traffic coming from our firewall can access the function app.


Based off the work done by: https://github.com/gamullen/FindNextCIDRRange/tree/main
