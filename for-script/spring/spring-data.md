<details>
  <summary>Why does Spring prefer unchecked exceptions?</summary>

- No Mandatory Catching
- Declarative Transactions: by default, transactions are rolled back only on unchecked exceptions
- Backward Compatibility: when modifying APIs, unchecked exceptions allow for adding new exceptions without breaking existing clients since clients are not forced to handle new exceptions
</details>

<details>
  <summary>What is the data access exception hierarchy in Spring?</summary>

- DataAccessException is the root of the hierarchy, and it provides a consistent approach to managing exceptions that arise from various data access technologies (e.g., JDBC, JPA, Hibernate). The DataAccessException class is an unchecked exception (extends RuntimeException).
- NonTransientDataAccessException - retrying the operation will not succeed without changing the cause of the exception.
- TransientDataAccessException - subsequent attempt might succeed without any intervention.
- etc.
</details>

<details>
  <summary>Name the approaches to implement data access in Spring Boot application</summary>

- JDBC - no Spring, doesn't handle connections
- Spring JdbcTemplate - opens and closes connections, catches exceptions, but doesn't handle transactions
- R2DBC - reactive, runs SQL queries
- ORM data access
</details>

<details>
  <summary>What is Spring JdbcTemplate?</summary>

The central class in Spring's JDBC support simplifies the use of JDBC and helps to avoid common errors.
- Uses a template pattern
- opens and closes connections
- execute SQL
- iteration over results
- catch and translate exceptions to DataAccessException
</details>


<details>
  <summary>Name JdbcTemplate callback interfaces</summary>

- RowMapper<T> - designed to map rows of a java.sql.ResultSet to instances of the specified generic type, it has a single method: T mapRow(ResultSet rs, int rowNum)
- RowCallbackHandler - designed for handling rows of a ResultSet, has a single method: void processRow(ResultSet rs)
- ResultSetExtractor - designed for extracting results from a ResultSet on a per-result basis. Unlike RowMapper<T>, which maps each row individually, ResultSetExtractor allows you to process the entire ResultSet in one go, providing more flexibility for complex result extraction logic, has a single method: T extractData(ResultSet rs)
</details>

<details>
  <summary>Explan types of handling transactions in Spring: Declarative and Programmatic</summary>

Declarative:
- most common approach in Spring applications
- separates transaction management from business code
- Annotation-Based Configuration, XML-Based Configuration

Programmatic:
- gives full control over the transaction boundaries within the code
- more flexible but also more complex and error-prone
- TransactionTemplate, TransactionManager, TransactionalOperation (Reactive)
</details>

<details>
  <summary>What is TransactionManager?</summary>

In Spring, a TransactionManager is a key component that coordinates and manages transactions. It is responsible for creating, committing, and rolling back transactions, as well as managing transaction resources such as database connections. 


TransactionManager is implemented by interfaces:
- PlatformTransactionManager - for synchronous operations. 
- ReactiveTransactionManager

Implementations of the PlatformTransactionManager interface:
- DataSourceTransactionManager - is used for managing transactions for JDBC-based applications.
- JpaTransactionManager is used to manage transactions in JPA-based applications. It integrates with the JPA EntityManagerFactory.
- JtaTransactionManager is used for managing transactions in Java EE environments where transactions span multiple resources (e.g., multiple databases, messaging systems). It is used for distributed transactions.

Implementations of the ReactiveTransactionManager:
- R2dbcTransactionManager - Manages transactions for R2DBC (Reactive Relational Database Connectivity) applications.
</details>

<details>
  <summary>What are the key methods for PlatformTransactionManager?</summary>

  Key Methods of PlatformTransactionManager:
- TransactionStatus getTransaction(TransactionDefinition definition): Begin a new transaction or return an existing one.
- void commit(TransactionStatus status): Commit the given transaction.
- void rollback(TransactionStatus status): Roll back the given transaction.
</details>

<details>
  <summary>Why JTA transaction approach is not frequently used and what is used in applications instead?</summary>

This approach is designed for managing distributed transactions across multiple resources, such as databases and messaging systems.
- Configuring JTA can be complex and requires a properly configured application server that supports JTA (e.g., JBoss, WebLogic, WebSphere)
- Managing distributed transactions involves significant overhead in coordinating multiple resources, which can impact performance and resource utilization.
- Modern applications often follow a microservices architecture where services are decoupled and communicate over REST APIs or messaging systems. In this architecture, distributed transactions are avoided due to their complexity, and eventual consistency patterns are preferred.
- For managing distributed data across microservices, patterns like Saga are often used, which provide a way to manage transactions without the need for a distributed transaction manager.
</details>

<details>
  <summary>What is TransactionDefinition in Spring?</summary>

In Spring, TransactionDefinition is an interface that provides a means to describe the properties of a transaction such as its propagation behavior, isolation level, timeout, and whether it is read-only:
- propagation: PROPAGATION_REQUIRED, PROPAGATION_REQUIRES_NEW, PROPAGATION_SUPPORTS, PROPAGATION_NOT_SUPPORTED, PROPAGATION_NEVER, PROPAGATION_MANDATORY, PROPAGATION_NESTED
- isolation: ISOLATION_DEFAULT, ISOLATION_READ_UNCOMMITTED, ISOLATION_READ_COMMITTED, ISOLATION_REPEATABLE_READ, ISOLATION_SERIALIZABLE
- timeout
- readOnly
</details>

<details>
  <summary>What readOnly is for?</summary>

- Database Performance: Some databases can optimize the execution of read-only transactions. They may skip certain checks and locks that are necessary for write operations, thus improving performance.
- Resource Management: Read-only transactions may consume fewer resources because they do not need to manage data changes, which can lead to faster execution times and reduced load on the database.

The database may use this hint to optimize the transaction. Optimizations can include:
- Skipping Locks: Avoiding the use of certain types of locks that are only necessary for write operations.
- Cache Optimization: Making better use of cache since no data modifications will occur.
- Reduced Logging: Minimizing the amount of transaction logging needed since no changes are being made.
- Resource Management: Allocating fewer resources since rollback operations for modifications are not needed.
</details>


<details>
  <summary>What is TransactionStatus in Spring?</summary>

TransactionStatus is an interface in Spring's transaction management framework that represents the current status of a transaction. It provides methods to control transaction behavior and query transaction state within a transactional context:
- isNewTransaction()
- hasSavepoint()
- setRollbackOnly()
- isRollbackOnly()
- flush()
- isCompleted()
</details>

<details>
  <summary>Name PlatformTransactionManager implementations</summary>

- DataSourceTransactionManager
- JpaTransactionManager - Suitable for applications using JPA with an ORM framework like Hibernate or EclipseLink.
- HibernateTransactionManager - Suitable for applications directly using Hibernate’s SessionFactory.
- JtaTransactionManager
- ChainedTransactionManager: For combining multiple transaction managers.
- ReactiveTransactionManager: For managing transactions in reactive programming models.
</details>

<details>
  <summary>What is ChainedTransactionManager?</summary>

ChainedTransactionManager is a specialized PlatformTransactionManager implementation provided by Spring Data that allows for combining multiple PlatformTransactionManager instances into a single coordinated transaction manager. This is useful when an application interacts with multiple transactional resources, and transactions are needed to be managed consistently across these resources.

When to Use ChainedTransactionManager
- Multiple Data Sources: When your application needs to interact with multiple data sources, ensure consistent transaction management across them.
- Mixed Resource Types: When combining different resource types, such as relational databases and messaging systems.
</details>



<details>
  <summary>How to enable declarative transaction management in Spring with annotations?</summary>

- Add Required Dependencies
- @EnableTransactionManagement on configuration class
- Use the @Transactional Annotation on classes or methods that are NOT private, static, final, or abstract. For JDK only public, for CGLIB proxy public, protected, and package-private 
</details>


<details>
  <summary></summary>
</details>








<details>
  <summary>What is Hibernate?</summary>

Hibernate is an ORM tool for Java that integrates with various transaction management strategies to handle database transactions.
HibernateTransactionManager implements the PlatformTransactionManager interface. 
</details>


<details>
  <summary>What is SessionFactory in Hibernate?</summary>

The SessionFactory is a central component in Hibernate that serves as a factory for Session objects. It is a thread-safe, heavyweight object designed for creating Session instances, which are used to interact with the database. The SessionFactory is typically created once during the application startup and reused throughout the application's lifecycle.
- The SessionFactory is built using configuration settings provided in a configuration file (hibernate.cfg.xml) or through a Configuration object in code. It is initialized with database connection settings, entity mappings, and various Hibernate properties.
- The primary responsibility of the SessionFactory is to provide Session instances. A Session represents a single unit of work with the database and is not thread-safe. SessionFactory is thread-safe and designed to be used concurrently by multiple threads.
- SessionFactory includes a level 2 (L2) cache, which is shared among all Session instances created by the SessionFactory. This helps improve performance by reducing the number of database queries.
</details>

<details>
  <summary>Levels of caching in Hibernate</summary>

</details>










