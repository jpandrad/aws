# Services Network Summary
These are the summaries of the AWS Network Service.

## VPC
1. VPC isolates computing resource from other computing resources available in the cloud;
2. VPCs are isolated to a region;
3. VPC CIDR block defines the IP addresses a VPC can use;
4. VPCs can have optional secondary IPv4 CIDR block as well IPv6 CIDR block;
5. Every region has a Default VPC with default subnets Security Groups, and NACLs;
6. The CIDR block for Default is 172.31.0.0/16;
7. The Default VPC and its subnets have outbound access to the internet by default;
8. One default subnet in each Availability Zone;
9. The Security Groups in default VPC allow outbound traffic and the NCALs are open in both inbound and outbound directions;


## Subnets
1. Subnets are a range of IP addresses within a VPC;
2. Subnets reside within a single Availability Zone;
3. Subnets can be made public/private using Internet Gateways and Nat Gateways;
4. Subnets can be configured for IPV4 and/or IPv6;
5. Subnets cannot overlap with other subnets in a VPC;


## Routing in VPC
1. Every VPC has a router which is responsible for routing traffic between subents as well as in and out of a VPC;
2. The router has an interface in every subnet of the VPC an is reachable from the network +1 address of each subnet;
3. Route table is a set of rules the router uses to foward network traffic - each rule is referred to as a route;
4. The router look at the destination IP of a packet leaving the subnet and will find a matching route by checking the destination column;
5. Once matched with a destination, the packet will be forwarded to the respective Target column of the route;
6. All toute tables have exctly one route by default, which is the local route (2 local routes will be created if IPV6 is enabled for VPC);
7. Every subnet is associated with one route table;
8. Each VPC has one default route table;
9. Multiple subnets can be associated with a single route table;