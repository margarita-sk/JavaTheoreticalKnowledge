<details>
  <summary>Why does Spring prefer unchecked exceptions?</summary>

- No Mandatory Catching
- Declarative Transactions: by default, transactions are rolled back only on unchecked exceptions
- Backward Compatibility: when modifying APIs, unchecked exceptions allow for adding new exceptions without breaking existing clients since clients are not forced to handle new exceptions
</details>

<details>
  <summary>What is the data access exception hierarchy in Spring?</summary>

Spring's DataAccessException is the root of the hierarchy, and it provides a consistent approach to managing exceptions that arise from various data access technologies (e.g., JDBC, JPA, Hibernate). The DataAccessException class is an unchecked exception (extends RuntimeException).
</details>
