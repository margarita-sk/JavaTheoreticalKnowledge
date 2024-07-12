<details>
  <summary>What is pessimistic and optimistic locking in DB?</summary>
  Pessimistic and optimistic locking are two strategies used in database management systems to handle concurrent access to data.

  1. Pessimistic locking assumes that conflicts between transactions are likely and thus:
- when a transaction wants to read or modify a record, it **locks the record**, preventing other transactions from accessing it until the lock is released.
- types of locks: Shared Lock (Read Lock) and Exclusive (Write lock)
- can lead to lower concurrency and potential bottlenecks, as transactions have to wait for locks to be released.

2. Optimistic locking assumes that conflicts are rare and thus takes a more lenient approach:
- do not lock records when reading. Instead, they check for conflicts only when attempting to commit changes
- typically involves a version check. Each record has a version number (or a timestamp) that is updated every time the record is modified. When a transaction attempts to update a record, it checks if the version number has changed since it was read
</details>


<details>
  <summary>Primary key vs Unique constraint?</summary>

Primary key: 
- is a unique identifier
- cannot be null
- only one per table
- automatically creates a unique index

Unique constraint: 
- ensures uniqueness of values in the column(s)
- can be null
- many per table
- automatically creates a unique index

</details>

