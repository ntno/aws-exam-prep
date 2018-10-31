#### tables
* 256 tables per region per account
* maximum item size 400 kb

**atomic counter**
* increment / decrement the value of an existing attribute without conflicting with other requests

**conditional write**
only write if the item's attributes meet expected conditions, otherwise error
available for:
* PutItem
* DeleteItem
* UpdateItem


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

#### query vs scan
* both support eventual consistent reads
* query returns all attributes on an item or selected attributes  
* query searches indexes only (more efficient)  

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
