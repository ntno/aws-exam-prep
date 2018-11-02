# SQS and SNS
## SQS - simple queue service
## SNS - simple notification service

*sns guarantees message delivery to sqs (but there can be duplicates)*

* 10 million subscriptions per topic    
* 100,000 topics per account  
  * higher limits by request  
* NO limit to # of queues

once component receives message, it will become invisible for 30 seconds (default VisibilityTimeout).  after that time it becomes visible again to other components unless it is deleted using DeleteMessage

setting VisibilityTimeout to 0 would make the message immediately visible

max time a message can live in sqs queue - 14 days  
min time - 1 min (assuming not deleted?)  
default time - 4 days    
*not sure why 14 days, is it 14 days or 12 hours?*


##### Fanout pattern
message published to SNS topic  
message distributed to a number of SQS queues in parallel
this allows you to take advantage of "parallel, asynchronous processing"  

Topic Name - 256 character limit (hyphens and underscores allowed), must be unique within account

subscriptions need to be confirmed before **3 days**, then the tokens for confirmation will expire

#### SNS Message
* Type
* MessageId - universally unique for each notification published
* TopicArn - ex: arn:aws:sns:us-west-2:12345692345:MyTopic
* Subject
* Message*
  * cannot be null/empty
  * JSON - can be used to specify different format per protocol
* Timestamp
* SignatureVersion
* Signature
* SigningCertURL
* UnsubscribeURL
* additional attributes
  * up to 10 per Message
  * all fields must be non null/empty
    * Name
    * Type
    * Value



#### SNS API for Owner
* CreateTopic
* DeleteTopic
* ListTopics (show all owned by a user by AWS ID)
* ListSubscriptionsByTopic
* SetTopicAttributes
* GetTopicAttributes
* AddPermission
* RemovePermission


#### protocols
* https (http over ssl)
* tls (transport layer security)
  * versions 1.0, 1.1, 1.2

#### integration with mobile
to push a notification to a mobile app you first have to register the app (platform, name, credentials) with Amazon  
then you create an endpoint for the app and mobile device
SNS sends notification messages to app and device

call the CreatePlatformEndPoint API to register multiple tokens

GCM - google cloud messsaging (??)
APNS - apple push notification service (??)


#### SQS Polling
##### long polling
* does not return a response until a message arrives or the poll times out
* can be used to reduce cost because you reduce the number of empty receives
* set ReceiveMessageWaitTimeSeconds to 20 seconds  


##### short polling
* returns immediately

#### SQS standard queue
* loose-FIFO but exact order is not guaranteed
  * tight-FIFO available in some regions
* message is delivered *at-least* once
* anonymous access is possible via IAM policies
* 1 million free requests per month
* message will be visible for a maximum of 12 hours
* you can specify what size messages are allowed in the queue (1kb - 256 kb) - SetQueueAttributes


#### dead letter queue
* receive message from other source queues
* receives messages that other queues can't process after some max # tries  

#### SNS endpoint
us east (north virginia): http://sns.us-east-1.amazonaws.com  
us west (north california): http://sns.us-west-1.amazonaws.com    
us west (oregon): http://sns.us-west-2.amazonaws.com   

other options:  
eu - europe [west, central,]  
ap - asia pacific [southeast, northeast,]  
sa - south america [east, ]  
