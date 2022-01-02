Available APIs:
- [[SQL]] - queries JSON objects, SQL queries are translated to [[Javascript]]
- Table - [[NoSQL]]
- [[Cassandra]] - NoSQL
- [[MongoDB]] - NoSQL, documents
- [[Gremlin]] - Graph database

Once selected, the API cannot be changed.
You can emulate CosmoDB locally

Partitions:
- CosmoDB stores your data on different servers called Partitions
- Partitions can be:
	- Logical: A portion of the CosmoDB container based on a condition. All items stored in a logical partition share the same *[[Partition Key]]*
	- Physical: A group of replicas of your data stored on the servers.

- Each logical partition has a limit of 20 GB.
- The partition key is how CosmoDB knows how to split the data into the logical partitions. Also, the partition key is immutable once you have selected it.
- The partition key must be chosen with performance in mind, frequent queries and the 20 GB limit per logical partition
- The partition key must be on fields that will never update and also have high cardinality (wide range of possible values), as an example `country`
- In situations where none of the object's properties can be used as a partition key, a synthetic one can be created by concatenating two properties, ex: `city-country` - "Oradea-Romania"

Consitency Levels:
- Strong: guarantees the most recent writes, highest cost
- Bounded staleness: linear writers, but with a defined delay
- Session: Balanced
- Consistent Prefix: linear writes with an undefined delay
- Eventual: No guaranteed write order, use this if data order does not matter in your app

Container Throughput:
- Dedicated: backed by SLA, has all the throughput
- Shared: the throughput is shared between all the containers marked as shared

Container Properties:
- Indexing policy: how items are indexed, define a custom behavior
- Time To Live (TTL): delete items after a period of time defined in seconds. Can be set on either the container or a specific item. If set on the container, every item in that container has the same TTL, unless specified a specific value for it.
	- A TTL of -1 means that it never expires
	- Setting a TTL on an item but not it's container will have no effect.