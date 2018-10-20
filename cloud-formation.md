Fn::GetAtt - returns the value of an attribute from a resource in the template

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

Ref Intrinsic Function
- use to assign values to properties which are not available until runtime
- can be used in:
  - resource properties
  - outputs
  - metadata attributes
  - update policy attributes
  - resources


  Resources - mandatory field in template
