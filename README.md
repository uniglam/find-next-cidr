# find-next-cidr
There is no built-in tool in Terraform to identify the next available space to create subnets in Azure virtual networks. This service (fa-uks-web-cidr-01) provides this missing functionality by returning the next available subnet range for a given CIDR (Classless Inter-Domain Routing) range.

Based off the work done by: https://github.com/gamullen/FindNextCIDRRange/tree/main
