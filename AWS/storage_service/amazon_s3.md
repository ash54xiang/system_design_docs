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

## S3 features
* Prefixes and Delimiters
  * Path/Folder1/[ObjectName], prefixes and delimiters are the terms for file hierachy in AWS (like folders structure in other platform)
* Storage classes
  * differnt class of storage including: 
    * Amazon S3 Standard ($$$$)
    * Amazon S3 Infrequent Access(IA) Storage ($$$)
    * Amazon S3 Reduced Redundancy Storage (RRS) ($$)
    * Glacier ($)
* Object lifecycle management
  * the objects stored in S3 standard can be moved to IA storage / Glacier eventually after some period of time without accessing it, this can further optimize the cost of storage
* Encryption
  * Server Side Encryption (SSE) - encryption happens after the files upload to the server (Insecure in transit)
  * Client Side Encryption -  encryption happens before uploading it to server (Secure in transit)
* Versioning
  * records and keeps the previous version of objects when new objects get uploaded into the bucket
* Multi-Factor Authentication (MFA) Delete
  * if someone would like to delete a file, he/she has to be holding MFA key
* Multi-parts Upload
  * upload big chunk of objects in smaller size in parallel
* Range GETs
  * specify a range of bytes from a big size of object to retrieve/access partial chunk of the object stored.
* Cross-Region Replication
  * replicate data from 1 region to another region to localize that bucket of data available in that region
* Logging
  * anything happened on the buckets gets logged
* Event Notification
  * send notification on any events happen on the buckets

## Tips
* Buckets' name has to be globally unique across the entire Amazon S3 (not just own account)
* 