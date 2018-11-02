# VPC - virtual private cloud
*virtual data centre in the cloud*
* 5 per region by default  
* default VPC - every account has them(?), default access to internet  
* peer VPC
  * connect VPCs via private IP addresses
  * hub/spoke, not transitive

### Internet Gateway
* 1 per VPC

### Virtual Private Gateway

### Route Table
which subnets are allowed to communicate to another subnet

### Network ACL  
* executed before security groups
* can block particular IPs
* NACL can be associated with multiple subnets
  * subnet can only be associated with 1 NACL
* inbound / outbound rules
  * private NACL have default deny on inbound and outbound
* cannot span VPCs
* default NACL that comes with the VPC allows inbound/outbound
* newly created NACL has default deny
* response to an inbound request subject to outbound rule (and vice versa)

#### Rules
rules are evaluated in numerical order

- number
  - ex: 100, 200
- type
  - ex: HTTP, HTTPS, SSH
- protocol
  - TCP (6), ALL
- port range
  - 80, 443, 22
- source
  - 0.0.0.0/0
- allow/deny

*allow ephemeral ports for outbound traffic only*

### subnet
* subnet spans 1 availability zone
* you can put subnets in different availability zones

#### IP range
10.0.0.0 - high address range
172.16.0.0 - medium
192.168.0.0 - small address range

CIDR
10.0.0.0/16 - ~65k unique IPs
10.0.0.0/24 - 256 IPs
10.0.0.0/28 - 16 IPs


### Security Group
* can span subnets
* allow access to certain ports
* allow different protocols (HTTP/HTTPS/SSH)



VPC can have an internal load balancer or an Internet-facing load balancer  
Internet-facing load balancers go in a *public* subnet  

* VPC usage is free
* connecting VPC to corporate datacenter using 'optional hardware VPN connection' - pricing is per hour the VPN connection is in an available state
* data transfer is charged  


#### ELB - Elastic Load balancer
DNS host name  
requests to host name are sent to a pool of EC2 instances  
Route 53 handles DNS on the backend

#### NAT (Network Address Translation)
**Instance**
- ec2 instance  
- use NAT AMI
- put in your public subnet  
- by default EC2 instances perform source/destination checks
  - the instance itself must be either the source or destination of any traffic  
  - NAT instance isn't the source or destination so you need to disable this check
- add route out of the instance in route table
  - now your resource in private subnet (?) can connect to internet to download files
- unfortunately this is not very scalable
- inside security group

**Gateway**
- gateway is created inside the public subnet
- not inside security group (?)
- 0.0.0.0/0 destination, target NAT gateway
  - can be used to allow instances in a **private subnet** to initiate outbound IPv4 traffic to the Internet but not vice versa
- per availability zone so you may need multiple for reliability
- no need to patch (more like a service)
- automatically assigned a public ip  
- no need to disable source/destination check  
- more secure than instance  

**Bastion server**  
use to ssh/rdp into private instance  
helps keep keys secure

#### elastic IP
* elastic IP - public static IPv4 address
  * can be quickly remapped to a different instance
* public IPv4 address can be reached by the Internet
* per region
* https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html
