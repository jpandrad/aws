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


## Internet Gateways
1. Enable resources to connect to internet;
2. Internet Gateways attach to a VPC and are region resilient;
3. VPC can only have max 1 internet gateway, and an internet gateway can onle be attached to max 1 VPC;
4. A subnet is made public once a default route point to the internet gateway in the VPC;


## NAT Gateways
1. NAT Gateways allow subnets to talk to the internet, but connections must be initiated from within the VPC;
2. NAT Gateways are deployed onto public Subnets so that they have a public IP and internet access;
3. Uses Elastic IPs;
4. AZ-reliant service need 1 NAT Gateway in each Availability Zone;
5. Route table for private subnets should point to NAT Gateway;
6. Managed by AWS;
7. Charged for wach hour that NAT gateway is available and for each Gigabyte of data that it processes;
8. A NAT gateway supports 5 Gbps of bandwidth and automatically scales up to 100 Gbps;



## Private and Public Subnets
1. Resources in public subnets are accessible to and from the internet;
2. Resources in private subnets are not accessible from the internet;
3. gateways determine whether a subnet is public or private;


