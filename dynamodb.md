# DynamoDB
*non relational database*

#### tables

https://www.tutorialspoint.com/dynamodb/dynamodb_indexes.htm  

https://dzone.com/articles/indexing-in-dynamodb

" Whenever a write occurs on a table, all of the table's indexes must be updated. In a write-heavy environment with large tables, this can consume large amounts of system resources. In a read-only or read-mostly environment, this is not as much of a concern—however, you should ensure that the indexes are actually being used by your application, and not simply taking up space."


* 256 tables per region per account
  * can be requested to be increased
* maximum item size 400 kb
* there are initial limits to throughput which can requested to be increased
  * US East (N. Virginia) has a bit higher than other regions
* items are stored across 10 GB partitions

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
primary key  
single attribute or composite
single attribute - partition key
composite - partition + sort key

partition key value used as input to a hash function which spits out location to store an item  

if using composite primary key, items with same partition key will be stored together (sort key must be unique within the partition)

data is stored based on the partition key element of the primary key...  
best to choose a partition key element with a large number of distinct values  
also try to ensure access is evenly distributed among the partitions

hash --- partition  
range --- sort

**Secondary Indexes**  
creates a shadow of the gold copy table but stores items according to a different index

| | Global     | Local     |
| :------------- | :------------- |
| **read options** | eventual consistency only      | eventual & strong       |
| **creation**| can be added at any time | only at table creation |
| **deletion**| can be deleted any time | never |
| **keys** | partition and sort can be different from those in base table| partition key must be the *same* as in the base table|
| **keys**| single or composite | composite only (must have partition and sort) |
| **size limit**| none | 10 GB total for a particular partition key |
| **query**| you can query/scan over the whole table | you can only query within a particular partition |
| **projection** | you can only retrieve attributes projected onto the index | you can retrieve attributes which have been projected *and* fetch additional attributes from the base table |
| **cost**| capacity is per index| capacity shared with the base table |
| **number per table** | 5 | 5 |   

*no increases in the max number of indexes on a table*



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

#### ProvisionedThroughputExceededException
if you exceed 3000 RCU or 1000 WCU for a particular partition, you may get throttled
causes:
hot key (one key is more frequently accessed)   
data not evenly distributed amongst partitions  
request rate > provisioned

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
* Scan can only retrieve 1 MB per call
  * use LastEvaluatedKey to pick up where you left off
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
BatchWriteItem
BatchGetItem
