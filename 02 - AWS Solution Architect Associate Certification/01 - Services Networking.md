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


## DNS
1. Device private IPs will automatically be assigned a DNS entry;
2. AWS DNS server can be accessed on the second IP of the VPC CIDR block as well - 169.254.169.253;
3. `enableDnsHostnames` - Determines whether the VPC supports assigning public DNS hostnames to instances with public IP addresses;
4. `enableDnsSupport` - Determines whether the VPC supports DNS resolution through the Amazon provided DNS server;


## Elastic IP
1. public IPs are not static and, if an EC2 instance goes down, then it will get a new public IP;
2. Elastic IPs are static IPv4 addresses that do not change;
3. To use an Elastic IP address, you first allocate one to your account, and then associate ir with your instance or network interface;
4. Elastic IPs are region specific and cannot be moved t oa different region;


## Security Groups and NACLs
### Security Groups, when there are no rules, block everythings
* When you add a security group rule, it allows a certain type of traffic;
* All security group rules "allow" traffic, there is no "deny" option for security groups;

### NACLs rules can either allow or deny traffic

### Summary
1. Stateless firewall required traffic to be explicitly permitted inbound and outbound;
2. Stateful firewalls are intelligent firewalls that track requests and allow response;
3. Network ACLs filter traffic enteriing and leaving a subnet;
4. Network ACLs are statless firewalls;
5. Security Groups act as firewalls for individual resources such as EC2, NICs, and other network objects;
6. Security Groups are stateful firewalls;
7. Security Group rules only "allow" traffic, whereas NACL rules have the option to "allow" or "deny";
8. Multiple Security Groups applied to a resrource will have their rules merged;
9. Every subnet within a VPC must be associated with a network ACL;
10. You can associate a network ACL with multiple subnets, however, a subnet can only be associated with only one network ACL at a time;


## Load Balancers
AWS have 3 Load Balanacers Types:
1. Classic Load Balancer
2. Aplication Load balancer
3. Network Load Balancer

### Classic Load Balancer (CLB)
* First load balancer introduced by AWS
* Not Recomended to use
* That it has a lot of limited features, one of those also happens to be specific to SSL, They only support one SSL certificate per Classic Load Balancer;


### Application Load balancer (ALB)
* Support HTTP/HTTPS/WebSockets;
* Function at the application layer (layer 7)
* Forward requests based off of:
    * URL Path conditions;
    * Host domain;
    * HTTP fields - header, method query and IP;
    * Supports HTTP redirect and custom HTTP response;
* Perform application-specific health checks;

### Networtk Load Balancer (NLB)
* Load balancer traffic based on TCP/UDP (layer 4);
* Meant for applications that don't use HTTP/HTTPS;
* Faster than Application load Balancers;
* Health check are only basic ICMP/TCP connections;
* NLB forwards TCP connections to instances;

### Summary
1. ELB auto-distributes incoming traffic across multiple targets in multiple Availability Zones;
2. Distributes traffic to EC2 instances, IPs, and Lambda functions;
3. Three types of ELB: Classic, Application, Network;
4. CLB are outdated nd should be avoided;
5. ALB functions on application layer and forwards HTTP/HTTPS traffic;
6. NLB can forward non-HTTP/HTTPS traffic;
7. NLBs are faster than ALBs;
8. HTTP/HTTPS is always terminated on ALB and not Network Load Balancer;
9. Cross-Zone Load balancing equally distributes traffic across all instances in all AZs;
10. A listener matches traffic based on rules and handles connection requests;
11. targert Groups route requests to registered EC2 instances based on specified protocol and port;


## VPN
### VPN Gateway Limits
* 1.25 Gbps Maximum Bandwidth per VPN tunnel;
* 140,000 Maximum packets per second;
* 1,466 Maximum transmission unit (MTU);

### Summary
1. Connect VPCs to on-primise data centers;
2. A virtual private gateway is the Amazon-side endpoint for your VPN, attachable to one VPC;
3. Customer Gateway is your side's physical device or software in a VPN connection;
4. Traverses over the public internet;
5. On-primise network can be set statically in a route table or dynamically exchanged via BGP;
6. charged per hour for every VPN connection as well as engress data out;
7. Max bandwidth 1.25 Gbps;


## Direct Connect
