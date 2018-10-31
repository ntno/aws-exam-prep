VPC can have an internal load balancer or an Internet-facing load balancer  
Internet-facing load balancers go in a *public* subnet  

* VPC usage is free
* connecting VPC to corporate datacenter using 'optional hardware VPN connection' - pricing is per hour the VPN connection is in an available state
* data transfer is charged  


#### ELB - Elastic Load balancer
DNS host name  
requests to host name are sent to a pool of EC2 instances  
Route 53 handles DNS on the backend
