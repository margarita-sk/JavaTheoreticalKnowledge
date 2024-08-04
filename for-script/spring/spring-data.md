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
  <summary>Name and explain @Transactional attributes</summary>

- propagation: defult=PROPOGATION_REQUIRED
- isolation: defult=ISOLATION_DEFAULT
- timeout
- readOnly: default=false
- rollbackFor : This attribute is an array of exception classes that should cause the transaction to rollback. By default, transactions will only rollback on unchecked exceptions (subclasses of RuntimeException) and Errors.
- rollbackForClassName
- noRollbackFor
- noRollbackForClassName
</details>

<details>
  <summary>Name and explain @EnableTransactionManagement attributes</summary>

- mode: default=AdviceMode.PROXY, AdviceMode.ASPECTJ
- proxyTargetClass: default=false; false: Uses JDK dynamic proxies, which create proxies based on interfaces; true: Uses CGLIB proxies, which create a subclass of the target class
- order: default=Ordered.LOWEST_PRECEDENCE; Ordered.LOWEST_PRECEDENCE: Ensures that the transaction advice is applied after other advices.
</details>


<details>
  <summary>What is the difference between PROPOGATION_REQUIRES, PROPOGATION_REQUIRES_NEW and PROPOGATION_NESTED?</summary>

Tx in Spring:
- physical tx
- logical tx

- PROPOGATION_REQUIRES: n logical tx within 1 physical tx
- PROPOGATION_REQUIRES_NEW: count(logical tx) = count(physical tx)
- PROPOGATION_NESTED: n logical tx within 1 physical tx, BUT with savepoints and rollback among each logical tx
</details>

<details>
  <summary>In JPA tests what is the default value to rollback? True or False? And how to change it?</summary>

The default is rollback true.
To Configure:
- @Rollback(false)
- @Commit
</details>


<details>
  <summary>What is JPA provider?</summary>

A JPA provider, also known as a JPA implementation, is a library or framework that implements the Java Persistence API (JPA) specification. The JPA specification itself is part of the Java EE (Enterprise Edition) platform and provides a standard way for Java applications to interact with relational databases. However, JPA is only a set of interfaces and guidelines; it does not provide the actual implementation. This is where JPA providers come into play.

Key Responsibilities of a JPA Provider:
- Mapping Java Objects to Database Tables: JPA providers handle the mapping between Java objects (entities) and database tables, including converting between different data types.
- Query Execution: They translate JPQL (Java Persistence Query Language) and Criteria API queries into SQL queries that the database can execute.
- Transaction Management: JPA providers manage transactions to ensure that database operations are executed consistently and reliably.
- Entity Lifecycle Management: They manage the lifecycle of entities, including operations such as persisting, merging, removing, and finding entities.
- Caching: Many JPA providers offer caching mechanisms to improve performance by reducing the number of database accesses.

When you use Spring Data JPA in your project, the default JPA provider it uses is Hibernate. This is because Hibernate is the most commonly used JPA implementation and is included as the default provider in Spring Boot's starter dependencies for JPA.
</details>

<details>
  <summary>Hibernate vs Spring Data JPA</summary>

Hibernate is a JPA implementation, while Spring Data JPA is a JPA Data Access Abstraction. 
</details>

<details>
  <summary>How do you configure a DataSource in Spring Boot?</summary>

application.properties or application.yml file for configuration
- spring.datasource.url=
- spring.datasource.username=
- spring.datasource.password=
- spring.datasource.driver-class-name=
</details>


<details>
  <summary>Is the JDBC template able to participate in an existing transaction?</summary>

Yes
```
    @Transactional
    public void performTransactionalOperation() {
        // This operation participates in the transaction started by @Transactional
        String sqlUpdate = "UPDATE my_table SET column_name = 'value' WHERE id = 1";
        jdbcTemplate.update(sqlUpdate);
        
        // Any other operations here will also participate in the same transaction
    }
```
</details>


<details>
  <summary>Which PlatformTransactionManager(s) can you use with JPA?</summary>

- JpaTransactionManager
- JtaTransactionManager
- DataSourceTransactionManager -  While primarily used for JDBC transactions, this transaction manager can sometimes be used in combination with JPA if JPA is configured to use a DataSource directly.
</details>


<details>
  <summary>What is a Repository interface in Spring?</summary>
A Repository interface in Spring Data JPA is a central part of the Spring Data framework that provides a mechanism for encapsulating storage, retrieval, and search behavior for a particular entity type.

- Domain-Specific
- Common Repository Interfaces: CrudRepository, PagingAndSortingRepository, JpaRepository
</details>


<details>
  <summary>What is @Query used for?</summary>
The @Query annotation in Spring Data JPA is used to define custom JPQL (Java Persistence Query Language) or SQL queries directly on repository methods. 
</details>

<details>
  <summary>What is @NamedQuery?</summary>

Purpose: Define static JPQL queries that can be referenced by name.
Usage: These annotations are used on entity classes to define predefined queries that can be executed from the entity manager.
</details>

<details>
  <summary>What is @EntityListeners?</summary>

The @EntityListeners annotation in JPA is used to specify one or more entity listener classes that will receive lifecycle events from the entity. These listeners can react to entity lifecycle events such as creation, update, and removal. 
</details>


<details>
  <summary>Explain JPA Method queries structure</summary>

The method names in Spring Data JPA repositories are composed of several parts:
- Keyword Prefix: Defines the type of query (e.g., find, read, get, query, count, delete, etc.).
- Limiting keywords that can be used are "first" or "top"
- Entity Property
- Condition: And, Or, Between, LessThan, GreaterThan, Like, etc.
- Numbers are allowed in the method name.
</details>















