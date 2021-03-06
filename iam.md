# IAM - Identity Access Management

## Policy Evaluation  

1) assume deny (default deny)
2) evaluate all policies  
3) was there an explicit deny?  if yes, then BLOCK  
4) was there an explicit allow?  if yes, then ALLOW
5) fall through to default BLOCK

## concepts
**user**  
represents person/service who uses the IAM user to interact with AWS   

**group**  
collection of IAM users  

**role**  
identity with permission policies - can be assumed by application (?)



#### accessing AWS from computer

1) create user  
2) attach permissions  
3) generate access keys  
4) make aws credentials file with keys or put   in user variables  


#### accessing AWS from EC2
1) create role  
2) attach permissions to role  
3) assign role to EC2 instance  
-> code executing on instance will assume the same permissions as the role

### authenticate against another identity system
#### Option 1
1) authenticate against LDAP (lightweight directory access protocol)  
2) retrieve the name of a IAM role associated with the user  
3) call the IAM Security Token Service to assume that IAM role  
4) use the temporary credentials ^  

#### Option 2
1) develop an identity broker which authenticates against LDAP  
2) call the IAM Security Token Service to get IAM federated user credentials  
3) use federated user credentials to access resource  


Federated User credentials
IAM Security Token service
