# Streams

## KStream

A KStream is an abstraction of a record stream, where each data record represents a self-contained datum in the unbounded data set. Using the table analogy, data records in a record stream are always interpreted as an **INSERT** -- think: adding more entries to an append-only ledger -- because no record replaces an existing row with the same key. Examples are a credit card transaction, a page view event, or a server log entry.

To illustrate, let's imagine the following two data records are being sent to the stream:

("alice", 1) --> ("alice", 3)

If your stream processing application were to sum the values per user, it would return 4 for alice. Why? Because the second data record would not be considered an update of the previous record. Compare this behavior of KStream to KTable below, which would return 3 for alice.

## KTable

A KTable is an abstraction of a changelog stream, where each data record represents an update. More precisely, the value in a data record is interpreted as an "UPDATE" of the last value for the same record key, if any (if a corresponding key doesn't exist yet, the update will be considered an INSERT). Using the table analogy, a data record in a changelog stream is interpreted as an **UPSERT** aka INSERT/**UPDATE** because any existing row with the same key is overwritten. Also, null values are interpreted in a special way: a record with a null value represents a "DELETE" or tombstone for the record's key.

To illustrate, let's imagine the following two data records are being sent to the stream:

("alice", 1) --> ("alice", 3)

If your stream processing application were to sum the values per user, it would return 3 for alice. Why? Because the second data record would be considered an update of the previous record.

**Effects of Kafka's log compaction**: Another way of thinking about KStream and KTable is as follows: If you were to store a KTable into a Kafka topic, you'd probably want to enable Kafka's log compaction feature, e.g. to save storage space.

## GlobalKTable

Like a KTable, a GlobalKTable is an abstraction of a changelog stream, where each data record represents an update.

A GlobalKTable differs from a KTable in the data that they are being populated with, i.e. which data from the underlying Kafka topic is being read into the respective table. Slightly simplified, imagine you have an input topic with 5 partitions. In your application, you want to read this topic into a table. Also, you want to run your application across 5 application instances for maximum parallelism. Then: 

- If you read the input topic into a **KTable**, then the "local" KTable instance of each application instance will be populated with data from only 1 partition of the topic's 5 partitions.
- If you read the input topic into a **GlobalKTable**, then the local GlobalKTable instance of each application instance will be populated with data from all partitions of the topic.