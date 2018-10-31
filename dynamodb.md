#### tables
* 256 tables per region per account
  * can be requested to be increased
* maximum item size 400 kb
* there are initial limits to throughput which can requested to be increased
  * US East (N. Virginia) has a bit higher than other regions

**atomic counter**
* increment / decrement the value of an existing attribute without conflicting with other requests

**conditional write**
only write if the item's attributes meet expected conditions, otherwise error
available for:
* PutItem
* DeleteItem
* UpdateItem

**Optimistic locking**
strategy to ensure that the client-side item you are updating/deleting is the same as the item in DynamoDB

hash --- partition  
range --- sort

#### Write Throughput
WCU - write capacity unit
1 write per second  
for a 1 kb item

* divide item size by 1kb, then round up to the nearest 1kb
* multiply by # items per second

#### Read Throughput
RCU - read capacity unit
1 strongly consistent read per second  
2 eventually consistent reads per second  
for a 4 kb items  

* round up item size to nearest 4kb, then divide by 4 kb
* multiply by # items per second
* if eventually consistent, divide by two

**you can reserve a minimum of 100 capacity units**

#### ProvisionedThroughputExceededException
can occur for a table or for one/more global secondary indexes  
GSI - the hash/partition is mandatory and the sort/range is optional  

#### query vs scan
* both support eventual consistent reads
* query returns all attributes on an item or selected attributes  
* query searches indexes only (more efficient)  
* if you do need to scan you can reduce the page size
  * or you could have scans done on a replica/shadow which doesn't take heavy traffic

#### indexes
5 global secondary indexes allowed
- can be added at OR after table creation
- can be deleted
5 local secondary indexes are allowed
- must be created at table creation time
- cannot be deleted
- support strong and eventual consistent reads
(10 total secondary indexes)
*no increases in index limit*


#### local secondary index
- same partition key as base table  
- different sort key from base table  
