SQS - simple queue service
SNS - simple notification service

##### Fanout pattern
message published to SNS topic  
message distributed to a number of SQS queues in parallel
this allows you to take advantage of "parallel, asynchronous processing"  

Topic Name - 256 character lymit (hyphens and underscores allowed)

subscriptions need to be confirmed before 3 days, then the tokens for confirmation will expire

#### SNS Message
* Type
* MessageId
* TopicArn
* Subject
* Message*
  * cannot be null/empty
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

to push a notification to a mobile app you first have to register the app (platform, name, credentials) with Amazon  
then you create an endpoint for the app and mobile device
SNS sends notification messages to app and device



#### SQS Polling
##### long polling
* does not return a response until a message arrives or the poll times out
* can be used to reduce cost because you reduce the number of empty receives
##### short polling
* returns immediately

#### SQS standard queue
* loose-FIFO but exact order is not guaranteed
* message is delivered *at-least* once
* anonymous access is possible via IAM policies
* 1 million free requests per month
* message will be visible for a maximum of 12 hours



#### SNS endpoint
us east: http://sns.us-east-1.amazonaws.com
us west (north california): http://sns.us-west-1.amazonaws.com  
us west (oregon): http://sns.us-west-2.amazonaws.com  

other options:
eu - europe
ap - asia pacific
sa - south america
