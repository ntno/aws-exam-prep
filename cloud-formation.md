# Cloud Formation  
**use this service to automatically provision resources**  
infrastructure as code  

max 200 stacks  
more can be requested by contacting AWS  
service is free
charged for resources
charged for errors
60 params max  
60 outputs max  


***
Fn::FindInMap  
- returns value corresponding to key in two-level map (from Mappings section)

Fn::Join  

Fn::Select  
- returns object from an array by index  
- index starts at 0!

Fn::GetAtt  
- returns the value of an attribute from a resource in the template
- typically used to generate outputs in the template

AWSTemplateFormatVersion - optional, identifies capabilities of AWSTemplateFormatVersion

latest template format version - "2010-09-09"


ListStackResources
- describes all resources in stack
- works on deleted stacks for up to 90 days

list-stacks
- get a list of any stacks you have created
- filterable by return status (CREATE_COMPLETE, DELETE_COMPLETE)
- returns name, stack id, template, status

describe-stacks
- provides info on running stacks  



python scripts
- cfn-init
- cfn-signal
- cfn-get-metadata
- cfn-hup

you can also install packages, files, services in a bootstrap scripts

Ref Intrinsic Function

- use to assign values to properties which are not available until runtime
- if you input the logical ID of ec2:eip then the public ip is returned
- can be used in:
  - resource properties
  - outputs
  - metadata attributes
  - update policy attributes
  - resources

Resources - mandatory field in template


CREATE_COMPLETE
CREATE_IN_PROGRESS


#### Amazon OpsWork
* configuration management service  
* uses Chef  
  * server configuration as code
