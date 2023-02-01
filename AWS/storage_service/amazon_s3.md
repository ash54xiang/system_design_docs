# Amazon Storage Services

1. Simple Storage Service (S3) - storage for objects (files)
2. Glacier
3. CloundFront
4. Elastic Block Store (EBS) - storage for blocks
5. Storage Gateway
6. Snow Family
7. Databases


## S3 Storage Overview
* Object storage
* Distributes across at least 3 Availability Zones
  * Except: 1A (1 zone, least expensive, less recoverable)
* Supports encryption and automatic data classification
* Big data analytics can run directly against stored data

## Getting Data into S3
* API
* Amazon Direct Connect
* Storage Gateway
* Kinesis Firehose
* Transfer Acceleration (based on cloud front tech)
* Snow Family
  * Snowball (box to carry data physically), Petabyte-scale
  * Snowball edge (smaller box than Snowball), 100TB local storage
  * Snowmobile (A mobile like a truck to carry the data), Exabyte-scale

## S3 Concepts
* Buckets - the containers to put objects into
* Regions - a physical location to put a bucket
* Objects - any forms of data including files, collections of data, etc.
* Keys  - logical names of the objects
* Objects URLs - link to the objects location
* Eventual consistency - the modified objects eventually get duplicated into other copies of buckets into other availability zones after a little of latency delay.

        Tips:
      * Objects in S3 buckets have eventual consistency
      * Objects in Elastic Block Stores are consistent
* Works great for static website hosting

## Common S3 Operations
* Creating and deleting buckets
* Writing, reading, deleting objects
* Managing object properties
* Listing keys in the buckets
* via REST interface as API