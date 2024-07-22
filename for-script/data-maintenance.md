<details>
  <summary>What is a transaction?</summary>
  Transaction is a logical unit of work that consists of database operations. It represents a single task or action that needs to be completed as an ACID operation.
</details>

<details>
  <summary>What is ACID?</summary>
  
1. **Atomicity**: either all the operations within a transaction are executed successfully, or if any operation fails, the entire transaction is rolled back, and the database is left unchanged.
2. **Consistency**: A transaction brings the data of the database from one consistent state to another. The data being modified or updated during the transaction should adhere to predefined **rules, constraints, and validations**. If a transaction violates any of these rules, the entire transaction is rolled back.
3. **Isolation**: Each transaction is isolated from other concurrent transactions executing concurrently in the system. This ensures that the intermediate states of a transaction are not visible to other transactions until the transaction is committed. Isolation prevents interference and maintains data integrity.
4. **Durability**: If we receive confirmation from the system that the transaction has been completed, we can be sure that the changes will not be canceled due to some failure like system power down, hardware failure, etc. This will not affect the completed transaction.
</details>

<details>
  <summary>Issues connected with the concurrent transactions</summary>

- **Lost Update**: occurs when two or more transactions concurrently access and modify the same data, resulting in one transaction's changes being overwritten or lost by another transaction. This situation can happen when transactions do not properly synchronize their updates. For example, if two transactions simultaneously read and update the same data without coordination, the changes made by one transaction may be lost when the other transaction commits its modifications.
- **Dirty Read**: A dirty read happens when a transaction **reads uncommitted** or intermediate data that has been modified by another transaction. In this scenario, a transaction reads data that has been changed **but not yet committed**. If the transaction that made the modifications rolls back, the data read by the initial transaction becomes invalid or incorrect. Dirty reads can lead to incorrect and inconsistent results.
- **Non-Repeatable Read**: A non-repeatable read occurs when a transaction reads the same data multiple times during its execution, but the data changes between the reads due to other concurrent transactions. This can result in inconsistent data, as the transaction sees different values for the same data within its execution. Non-repeatable reads can happen when a transaction reads a row, another transaction modifies the same row, and then the first transaction reads the row again, observing the updated value.
- **Phantom Read**: Phantom reads involve a transaction reading a set of data rows that satisfy a certain condition, and then, during a subsequent read, finding additional rows that meet the same condition due to concurrent transactions. In other words, phantom reads occur when new rows appear or disappear between two reads within the same transaction, causing the result set to change unexpectedly. This phenomenon typically arises when a transaction performs range-based queries and concurrent transactions insert or delete rows within that range.
</details>


<details>
  <summary>List and explain levels of isolation of transactions</summary>
  
- READ_UNCOMMITTED
- READ_COMMITTED - solves dirty read
- REPEATABLE_READ - solves non-repeatable read
- SERIALIZABLE - solves phantom read
</details>

<details>
  <summary>What is Propagation?</summary>

Propagation defines the behavior of the transaction when one transactional method calls another transactional method. It specifies whether the called method should participate in the existing transaction or should create a new independent transaction. Different propagation options are available, and the specific behavior depends on the chosen propagation level.

|  | if transaction exists | If no transaction exists |
| --- | --- | --- |
| REQUIRED (default) | join | create new |
| REQUIRES_NEW | create new | create new |
| SUPPORTS | join | is executed non-transactionally |
| NOT_SUPPORTED | suspend transaction execute non-transactionally | is executed non-transactionally |
| MANDATORY | join | throws exception |
| NEVER | throws exception | is executed non-transactionally |
| NESTED | marks a save point (f our business logic execution throws an exception, then the transaction rollbacks to this save point) | create new |
</details>

<details>
  <summary>What is sequence?</summary>

A sequence provides a systematic way of generating sequential numbers that are guaranteed to be unique within a database.

- A sequence is defined and **managed by the database** management system (DBMS). Each DBMS may have its own specific syntax and implementation for sequences.
- A sequence is independent of any specific table or column. It is a **standalone database object** that can be referenced by multiple tables or columns within a database.
- Sequences generate numeric values in a sequential order based on a specified increment value. The increment value determines how much the sequence value is increased with each invocation.
- The generated sequence values are typically used for populating primary key columns of tables, ensuring that each new record gets a unique identifier.
- Sequences provide an efficient and scalable way of generating unique numeric values, especially in scenarios where multiple concurrent transactions are inserting data into the database.
- The specific range and behavior of a sequence, such as its starting value, minimum value, maximum value, and increment value, can be configured during its creation.
</details>


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

<details>
  <summary>What are indexes and how do they work?</summary>

Data structures that improve the speed and efficiency of data retrieval operations.

- Speed Up Queries: Indexes are used to quickly locate and retrieve data from a database without having to scan every row in a table. This significantly reduces the time needed for search queries and improves performance.
- Optimize Performance: By creating indexes on columns that are frequently used in search conditions, sorting, and joining operations, database performance can be greatly enhanced.

Data Structure: Indexes are usually implemented as data structures like B-trees (Balanced Trees) or hash tables. These structures allow for fast data access and retrieval.
</details>


<details>
  <summary>What is deadlock?</summary>
it refers to a situation where two or more database transactions are waiting indefinitely for each other to release resources, resulting in a state of mutual deadlock. This deadlock prevents any of the involved transactions from progressing further, leading to a potential system freeze or significant performance degradation.
</details>


<details>
  <summary>What is JPA?</summary>
JPA stands for Java Persistence API. It is a Java specification that defines a standard way to manage relational data in Java applications using Object-Relational Mapping (ORM). JPA provides a high-level abstraction layer over relational databases, allowing developers to work with Java objects rather than writing low-level SQL queries.  
</details>

<details>
  <summary>What are the key components of JPA?</summary>

1. **Entity Classes**: JPA maps database tables to Java classes known as entity classes. An entity class represents a table row, and each instance of the class corresponds to a row in the database table.
2. **EntityManager**: EntityManager is the central interface in JPA for managing entities. It provides methods for performing CRUD (Create, Read, Update, Delete) operations, querying the database, and managing transactions.
3. **Persistence Unit**: A persistence unit is a configuration file (persistence.xml) that defines the properties and settings for the JPA implementation. It specifies the database connection details, mapping information, and other configuration options.
4. **Object-Relational Mapping configuration:** JPA uses **annotations** or XML configuration to define the mapping between entity classes and database tables. It allows developers to specify how fields and relationships in Java objects are mapped to columns and tables in the database.
5. **JPQL**: JPA provides a powerful query language called Java Persistence Query Language (JPQL). JPQL is similar to SQL but operates on Java objects and entity relationships instead of database tables. It allows developers to write portable and **database-independent queries**.
</details>


<details>
  <summary>Name JPA features</summary>

In addition to these basic CRUD operations, JPA also provides other operations and features, such as:

- **Relationships**: JPA allows you to define relationships between entities, such as one-to-one, one-to-many, many-to-one, and many-to-many relationships. You can use annotations like @OneToOne, @OneToMany, @ManyToOne, and @ManyToMany to establish and manage these relationships.
- **Cascading Operation**s: JPA supports cascading operations, where changes in the state of one entity can automatically propagate to associated entities. For example, when you persist an entity that has a related entity, you can configure JPA to persist the related entity as well.
- **Transaction Management**: JPA integrates with Java EE or Spring transaction management to ensure data consistency and integrity. You can use annotations like @Transactional to define transactional boundaries and manage database operations within a transaction.
- **Querying**: JPA provides various options for querying data, including JPQL (Java Persistence Query Language), Criteria API, and native SQL queries. These querying mechanisms allow you to retrieve and manipulate data based on specific conditions and criteria.
</details>


<details>
  <summary>What is ORM?</summary>
  ORM stands for Object-Relational Mapping. It is a programming technique used to map objects in an object-oriented programming language to relational database tables. The purpose of ORM is to bridge the gap between the object-oriented paradigm used in application code and the relational database model used for data storage.

In traditional database systems, data is stored in tables with rows and columns. However, in object-oriented programming, data is represented as objects with properties and methods. ORM provides a way to interact with databases using objects, allowing developers to work with familiar object-oriented concepts and techniques.
</details>


