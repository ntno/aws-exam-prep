# DynamoDB

#### tables
* 256 tables per region per account
  * can be requested to be increased
* maximum item size 400 kb
* there are initial limits to throughput which can requested to be increased
  * US East (N. Virginia) has a bit higher than other regions

**atomic counter**
* increment / decrement the value of an existing attribute without conflicting with other requests
* all write requests will be executed in the order they are received

**conditional write**
only write if the item's attributes meet expected conditions, otherwise error
available for:
* PutItem
* DeleteItem
* UpdateItem

**Optimistic locking**
strategy to ensure that the client-side item you are updating/deleting is the same as the item in DynamoDB

***
data is stored based on the partition key element of the primary key...  
best to choose a partition key element with a large number of distinct values  
also try to ensure access is evenly distributed among the partitions

hash --- partition  
range --- sort

#### Write Throughput
**WCU - write capacity unit**  
1 write per second for a 1 kb item

* divide item size by 1kb, then round up to the nearest 1kb
* multiply by # items per second

#### Read Throughput
**RCU - read capacity unit**  
1 strongly consistent read per second  
2 eventually consistent reads per second  
for a 4 kb items  

* round up item size to nearest 4kb, then divide by 4 kb
* multiply by # items per second
* if eventually consistent, divide by two

*you can reserve a minimum of 100 capacity units*

#### ProvisionedThroughputExceededException (??)
can occur for a table or for one/more global secondary indexes  
GSI - the hash/partition is mandatory and the sort/range is optional  

***

#### query vs scan
* *both* support eventual consistent reads
* query returns all attributes on an item or selected attributes  
* query searches indexes only (more efficient)  
* query returns items matching the primary key search
* if you do need to scan you can reduce the page size
  * or you could have scans done on a replica/shadow which doesn't take heavy traffic
* query uses primary key of the table or a secondary index... ??
* you can use a KeyConditionExpression to only look in a particular partition  

#### indexes
5 global secondary indexes allowed
- can be added at OR after table creation
- can be deleted
- partition key and sort key CAN be different from those of the base table
- 'global' means that queries can span all data in the base table, across all partitions

5 local secondary indexes are allowed
- must be created at table creation time
- cannot be deleted
- support strong and eventual consistent reads
- partition key SAME as that of base table
- sort key DIFFERENT from that of base table  
- 'local' because every partition is scoped to a base table partition with the same partition key value (??)
 - supports strong and eventually consistent reads

(10 total secondary indexes)  
*no increases in index limit*

***

BatchGetItem   
- returns attributes for multiple items (can be accross tables)  
- request by primary key
- 100 items max
- up to 16 MB data in one call

Item Collection  
- maximum size of collection is 10 GB
- rule applies to tables with 1 or more local secondary indexes
- 'for any distinct partition key value the sum of the items in the table plus the sum of the items across its local secondary indexes must not exceed 10 GB'

CreateTable  
UpdateTable  
UpdateItem  
ListTables  
