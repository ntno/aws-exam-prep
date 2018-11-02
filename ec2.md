# EC2 - elastic compute cloud

#### elastic IP
static IPv4 address for *dynamic* cloud computing  
associated with your AWS account  
can be used to mask failure by remapping to another instance in your AWS account  
public IP

#### AMI - Amazon Machine Image
* you can share with a specific AWS account by account ID  
* you can make public  
* AMIs are **regional**  
  * to make it available in a different region you would use CopyImage action
* after you create the AMI you have to register it before you can launch it using the RegisterImage API  
* DescribeImages API describes one or more images
* RunInstances to start, returns DNS names
* DescribeInstances - status on running ec2 instances
* TerminateInstances
* StopInstances - release compute resources but preserve data on the EBS boot partition
* StartInstances - restart instance associated with ^ EBS boot partition  

***

root device data can go on an Amazon EBS or a local instance store   
EBS - data will persist independent from the lifetime of the instance  
Instance - data only stored for lifetime of the instance  

#### Amazon Instance Store-Backed
* boot time usually less than 5 min  
* max size 10 GB
* data persists during life of the Instance  
  * instance can be rebooted
  * data will NOT be persisted if stopped
  * data will NOT be persisted if terminated

#### Amazon EBS-Backed
* boot time usually less than 1 min  
* max size 16 TB
* default:
  * root volume deleted when instance terminated (by default)
  * other volumes persist when instance terminated
* instance type / kernel / RAM etc for instance can be changed while instance is stopped without affecting data in the EBS-backend

#### SSH
`chmod 0400 LAFile.pem`  
`ssh -i LAfile.pem ec2-user@52.2.222.22`    
*permissions of 0777 allow anyone to read/write*  

SSH uses port 22  
Windows RDP uses port 3389


#### instance metadata
instance knows its own metadata
* ami-id
* ami-launch-index
* ami-manifest-path
* block-device-mapping/
* hostname
* instance-action
* instance-id
* instance-type
* kernel-id
* local-hostname
* local-ipv4
* mac
* network/
* placement/
* public-hostname
* public-ipv4
* public-keys/
* reservation-id
* security-groups
* services/
