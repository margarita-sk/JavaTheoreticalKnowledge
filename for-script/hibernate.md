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
