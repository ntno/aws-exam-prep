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
* can be used to allow instances in a **private subnet** to initiate outbound IPv4 traffic to the Internet but not vice versa (NAT instance must be in a **public subnet**)
  * source/destination checks should be disabled in this case


#### elastic IP
* elastic IP - public static IPv4 address
  * can be quickly remapped to a different instance
* public IPv4 address can be reached by the Internet
* per region
* https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html
