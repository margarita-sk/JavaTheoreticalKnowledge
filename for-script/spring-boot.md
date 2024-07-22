<details>
  <summary>What is Spring Boot?</summary>

Spring Boot is an open-source framework designed to simplify the development of Spring-based applications.

Key Features
- Auto-Configuration: Automatically configures your application based on the dependencies you include, reducing boilerplate code.
- Embedded Servers: Comes with embedded servers like Tomcat or Jetty, allowing you to run applications as standalone executable JARs (not WARs).
- Microservices Support: Ideal for building microservices with features from Spring Cloud.
- Production-Ready: Includes Actuator for monitoring and managing applications, and supports externalized configuration for different environments.
- Developer Tools: Spring Initializr helps quickly generate Spring Boot projects with necessary dependencies.

Benefits
- Reduced Configuration: Uses sensible defaults to minimize the need for manual setup.
- Simplified Deployment: Runs on embedded servers, making it easy to deploy anywhere.

Cons:
- Memory Consumption
- Startup Time
</details>

<details>
  <summary>Why Spring Boot is called "opinionated"?</summary>
  Spring Boot is considered "opinionated" because it provides a set of conventions and default configurations that guide developers towards best practices and streamline the development process.
</details>

<details>
  <summary>What things affect what Spring Boot sets up?</summary>

- Dependencies: The libraries included in your pom.xml or build.gradle files trigger specific auto-configurations.
- Properties: Settings in application.properties or application.yml override default configurations.
- Environment: Profiles and environment-specific configurations can alter setups.
</details>

<details>
  <summary>Can you control logging with Spring Boot? How?</summary>

application.properties: 
logging.level.root=INFO
logging.level.org.springframework.web=DEBUG
logging.file.name=myapp.log
logging.pattern.console=%d{yyyy-MM-dd HH:mm:ss} - %msg%n
Spring Boot uses Logback by default. You can customize Logback settings with a logback-spring.xml or logback.xml file in the src/main/resources directory.

</details>

<details>
  <summary>How do you access the properties defined in the property files?</summary>

- @Value("${my.property.key}") - on field level
- @ConfigurationProperties(prefix = "my") - on class level - on bean
- env.getProperty("my.property.key");

</details>


<details>
  <summary>What properties do you have to define in order to configure external DB?</summary>

- spring.datasource.url: The JDBC URL for connecting to the MySQL database, including the hostname, port, and database name.
- spring.datasource.username: The username used to authenticate with the MySQL database.
- spring.datasource.password: The password used for authentication.
- spring.datasource.driver-class-name: The JDBC driver class name. For MySQL, this is typically com.mysql.cj.jdbc.Driver.
- spring.jpa.database-platform: Hibernate dialect for MySQL. This helps Hibernate generate SQL optimized for MySQL.
- spring.jpa.show-sql: If true, SQL statements will be logged to the console.
- spring.jpa.properties.hibernate.format_sql: If true, SQL statements will be formatted for readability.
</details>
