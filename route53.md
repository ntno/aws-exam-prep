## DNS - domain name system
**used to convert human friendly domain names to a IP address**

IPv4 - 32 bit field, 4 billion addresses
IPv6 - 128 bit field, 340 undecillion addresses


## Domain
last word is the 'top level domain name'  
- .com  
- .edu  
- .gov  

top level governed by IANA

second word is the 'second level domain name'  
- the .gov part in .gov.uk

### Domain Registrar
can assign domains within a top level domain name

## Routing Policy  
### Simple  
* default
* commonly used when you have 1 resource
* user -> route53 -> your resource
* round robin

### Weighted
* a/b testing
* slowly ramp up traffic to new version  

### Latency

### Failover
* send to disaster recovery if main site fails health check

### Geolocation
* based on closest resource

***

**A record**
(A is for address)
* points to an IP address

NOTE  
elastic load balancer always just has a DNS name, no IPv4 or IPv6  
you can't use an A record to resolve to the ELB  
you would need an alias record for this

**TTL** - time to live for a DNS record to be cached  
the lower the time, the faster changes to DNS records will propagate throughout the internet

**CNAME** - canonical name
used to resolve one domain name to another  
mobile.acloud.guru could resolve to m.acloud.guru  

**Alias Record** - Amazon/Route53 specific
maps DNS name to a target DNS address (?)
* typically used to map to an ELB
* for exam Alias > CNAME

ELB  
- you can never have a public IP address for this
- no IPv4 address
- ELB can only be resolved using DNS name
