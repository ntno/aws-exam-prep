#### elastic IP
static IPv4 address for *dynamic* cloud computing  
associated with your AWS account  
can be used to mask failure by remapping to another instance in your AWS account  

#### public IP
#### AMI - Amazon Machine Image
* you can share with a specific AWS account by account ID  
* you can make public  
* AMIs are *regional*  
* after you create the AMI you have to register it before you can launch it using the RegisterImage API  
* DescribeImages API describes one or more images


#### Amazon Instance Store-Backed
* boot time usually less than 5 min  
* max size 10 GB
* data persists during life of the Instance  
  * instance can be rebooted
  * instance can NOT be stopped
  * instance can NOT be terminated

#### Amazon EBS-Backed
* boot time usually less than 1 min  
* max size 16 TB
* default:
  * root volume deleted when instance terminated
  * other volumes persist when instance terminated

#### SSH
`chmod 0400 LAFile.pem`  
`ssh -i LAfile.pem ec2-user@52.2.222.22`    
*permissions of 0777 allow anyone to read/write*  
