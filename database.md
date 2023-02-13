# Sharding / Data Partitioning

## Types of Database
1. Relational Database - focus on **ACID** (*Atomicity, Consistency, Isolation, Durability*)
   * Strength:
     * Reliable
     * Consistent
     * Execellent integrity
   * Time Considerations:
     * More time defining schema
     * Potentially slower to market
     * Complex queries
   * Money Considerations:
     * Often expensive at scale
     * Queries easier = less expensive to write
   * Examples:
     * PostgreSQL
     * MySQL
     * MariaDB
     * MS SQL
     * Oracle
2. NoSQL (Not only SQL) Databse - focus on **BASE** (*Basically Available, Soft state, Eventual Consistency*)
   * Strength:
     * Scalable
     * Flexible
     * Fast
   * Time Considerations:
     * Less time upfront / agile
     * Often associated with agile - rapid development
     * Developers often tasked with writing own code to help with consistency
   * Money Considerations:
     * Can be expensive with server sprawl
     * Potentially more affordable
       * depends on the added complexity of system
   * Examples:
     * Document DB - JSON-like format (BSON, binary JSON)
       * MongoDB
       * CouchDB
     * Time Series
       * InfluxDB
       * TimeScale
     * Real time
       * Firebase
       * RethinkDB
     * Wide-Column DB - large amounts of data with predefined queries, subset of key-value
       * Cassandra
       * HBase
     * Key-Value - key value paired format
       * Redis
       * DynamoDB
     * Graph DB - multidimensional relationships, navigating patterns in different datasets
       * Neo4j

* **Note:** Relational DB fits Consistency in CAP theorem, but to achieve Availability and Partition Tolerance, NoSQL thrives into the use cases.
* Example of NoSQL use cases:
  1. Caching
  2. User sessions
  3. Real-time inventory
  4. Fraud mitigation
* Example of relational SQL use cases:
  1. Banking system
  2. Accounting
  3. Complex SQL queries
  4. Smaller system
## Partitioning Method

* Horizontal partitioning - aka Sharding
* Vertical partitioning