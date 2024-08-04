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
</details>

<details>
  <summary>How to configure default schema and initial data?</summary>

- Configuring Default Schema: spring.jpa.properties.hibernate.default_schema=<schema-name>
- Configuring Initial Data: A file named schema.sql or data.sql can be placed in the src/main/resources directory to initialize the database schema or data.
- For unit tests, you can use the @Sql annotation to execute SQL scripts before or after a test method:     @Sql("/test-data.sql")
</details>

<details>
  <summary>What is a fat jar? How is it different from the original jar?</summary>
Fat jar includes application classes + all dependencies. Can be run directly with java -jar, self-contained.
</details>

<details>
  <summary>What is the difference between an embedded container and a WAR?</summary>

- Embedded Container: A server that is bundled within the application itself (e.g., Tomcat, Jetty, or Undertow). The application is packaged as a standalone JAR file that includes the server. No need for an external application server. Ideal for microservices and standalone applications. Simplifies deployment and configuration.
- WAR: Requires an external server to deploy and run. Used in traditional server environments.
</details>


<details>
  <summary>What embedded containers does Spring Boot support?</summary>
  
- Jetty
- Tomcat
- Undertow
</details>


<details>
  <summary>Explane annotation: @SpringBootApplication</summary>
Level: class
Functionality: Combines @EnableAutoConfiguration, @ComponentScan, and @Configuration. Configures and launches a Spring Boot application.
</details>

<details>
  <summary>Explane annotation: @EnableAutoConfiguration	</summary>
Level: class
Functionality: Enables Spring Boot’s auto-configuration feature. Automatically configures the Spring application context based on the dependencies that are present on the classpath. It scans the classpath for available beans and settings, then configures them to reduce the need for explicit bean definitions in your configuration.
</details>

<details>
  <summary>Explane annotation: @ConfigurationProperties	</summary>
Level: Class, Field
Functionality: Binds external configuration properties to a Java object.
</details>

<details>
  <summary>Explane annotation: @PropertySource</summary>
Level: Class
Functionality: Specifies the location of property files.
</details>


<details>
  <summary>Explane annotation: @RestController	</summary>
Level: Class
Functionality: @Controller + @ResponseBody
</details>

<details>
  <summary>Explane annotation: @AutoConfigurationPackage	</summary>
Level: Class
Functionality: Specifies the package to scan for auto-configuration.
</details>



<details>
  <summary>Explane annotation: @TestConfiguration and @TestPropertySource	</summary>
Level: Class
Functionality: Defines test-specific configuration and Provides a way to configure properties for test contexts.
</details>


<details>
  <summary>Explane annotation: @SpringBootTest	</summary>
Level: Class
Functionality: Provides support for integration testing of Spring Boot applications. Contains @BootstrapWith(SpringBootTestContextBootstrapper.class)
+ @ExtendWith({SpringExtension.class})
</details>


<details>
  <summary>Explane annotation: @DataJpaTest</summary>
Level: Class
Functionality: Configures an in-memory database and scans for JPA repositories.
</details>

<details>
  <summary>Explane annotation: @WebMvcTest</summary>
Level: Class
Functionality: Configures a slice test for Spring MVC controllers.
</details>

<details>
  <summary>Explane annotation: @WebFluxTest</summary>
Level: Class
Functionality: Configures a slice test for Spring WebFlux controllers.
</details>



<details>
  <summary>List and explain conditionalOn annotations </summary>
Level: Class, method

- @ConditionalOnClass(name = "com.example.SomeClass")
- @ConditionalOnBean(name = "dataSource")
- @ConditionalOnMissingBean(DataSource.class)
- @ConditionalOnMissingClass(value = "com.example.SomeClass")
- @ConditionalOnProperty(name = "feature.enabled", havingValue = "true")
- @ConditionalOnWebApplication
- @ConditionalOnResource(resources = "classpath:somefile.txt")
- @ConditionalOnExpression("${some.expression:true}")
- @ConditionalOnJava(JavaVersion.EIGHT)

</details>


<details>
  <summary>Where does Spring Boot do component scanning by default?</summary>
When you use the @SpringBootApplication annotation, it implicitly includes the @ComponentScan annotation.
By default, Spring Boot scans for components (classes annotated with @Component, @Service, @Repository, @Controller, etc.) in the package where the @SpringBootApplication annotated class is located and all its sub-packages.
</details>


<details>
  <summary>How to configure DataSource and JdbcTemplate in Spring Boot application?</summary>

Spring Boot automatically configures a DataSource based on dependencies and application properties:
1. Dependency Inclusion: include spring-boot-starter-data-jpa and DB driver dependency
2. Define the necessary properties: spring.datasource.url, spring.datasource.username, spring.datasource.password, spring.datasource.driver-class-name
3. Spring Boot’s DataSourceAutoConfiguration class detects the presence of the DataSource properties and automatically configures a DataSource bean using these properties.

Spring Boot’s JdbcTemplateAutoConfiguration class automatically configures a JdbcTemplate bean if a DataSource bean is available.
</details>


<details>
  <summary>What is spring.factories file for?</summary>

The spring.factories file is used by Spring Boot to enable auto-configuration and other types of configuration in a modular and extensible way.
We can specify our own spring.factories file. But also, each spring-boot dependency contains it in META-INF folder. This file is used to register auto-configuration classes and other configurations necessary for the starter to function correctly.
</details>


<details>
  <summary>What features does Spring Boot Actuator provide?</summary>

1. Endpoints enabled by default:
- /actuator/health
- /actuator/info

2. Endpoints disabled by default:
- /actuator/beans
- /actuator/env
- /actuator/loggers
- /actuator/metrics
- /actuator/mappings
- /actuator/threaddump 
- /actuator/heapdump
- /actuator/httptrace
- /actuator/mappings

to enable management.endpoints.web.exposure.include=health,info,metrics

3. Also we can customize our own actuator endpoint.
4. Integration with External Monitoring Systems: Prometheus, Micrometer
  
</details>


<details>
  <summary>What protocols can be used to access actuator endpoints?</summary>
HTTP and JMX
</details>

<details>
  <summary>What is info endpoint for?</summary>
  
  The info endpoint in Spring Boot Actuator is used to expose arbitrary application information. This endpoint can be used to provide details about the application, such as:
  - Version number
  - Build information
  - Description
  - Custom application-specific information

Supplying Data to the info Endpoint:
- Add key-value pairs under the info prefix in your configuration file: info.app.name=My Application
- Implement the InfoContributor interface to add custom information programmatically.
</details>


<details>
  <summary>How to change logging level of a package using loggers endpoint?</summary>
POST .../actuator/loggers/com.example.myapp -H "Content-Type: application/json" -d '{"configuredLevel": "DEBUG"}'
</details>


<details>
  <summary>What are metrics for?</summary>

The metrics endpoint in Spring Boot Actuator provides detailed information about the application's performance and resource usage, such as:
- JVM metrics (heap memory, garbage collection)
- System metrics (CPU usage, memory usage)
- Custom application metrics
</details>

<details>
  <summary>How to access an endpoint using a tag?</summary>

You can use tags to filter and group metrics. Common tags include:
- application (e.g., application:myApp)
- status (e.g., status:up, status:down)
- region (e.g., region:us-west, region:eu-central)

Example URL with Tags:
http://localhost:8080/actuator/metrics/jvm.memory.used?tag=area:heap
</details>

<details>
  <summary>How to create a custom metric with or without tags?</summary>
  
In Spring Boot, you can create custom metrics using the MeterRegistry provided by Micrometer.
Creating a Custom Metric: inject MeterRegistry 
1. Without Tags: meterRegistry.counter("custom.metric").increment();
2. With Tags: meterRegistry.counter("custom.metric", "type", "example", "status", "success").increment(); In this example, "type" and "status" are tags with values "example" and "success".
</details>

<details>
  <summary>What is Health Indicator in Spring Boot?</summary>

 Health Indicator is a component that provides health information about an application or a particular part of it. Health Indicators contribute to the overall health status exposed by the /actuator/health endpoint, helping to monitor the application's health and diagnose issues.

Key Features:
- Health Check Integration: Health Indicators are automatically integrated into the Spring Boot Actuator's health endpoint.
- Customizable: You can create custom health indicators to check the health of specific parts of your application.

Custom health indicator: implements HealthIndicator
</details>


<details>
  <summary>What are the Health Indicators that are provided out of the box?</summary>

  Built-in Health Indicators:
- Database: Checks the status of database connections.
- Disk Space: Monitors available disk space.
- Message Brokers: Checks the status of messaging systems like RabbitMQ, Kafka, etc.

These health indicators are automatically included when you add the relevant dependencies to your project.
</details>


<details>
  <summary>What is the Health Indicator status?</summary>

In Spring Boot, the Health Indicator status is an indicator of the overall health of a specific component or the entire application. 
- UP: The component or application is healthy and operating as expected.
- DOWN: The component or application is not healthy and is experiencing issues.
- OUT_OF_SERVICE: The component or application is intentionally taken out of service and should not be used.
- UNKNOWN: The health status of the component or application cannot be determined.


The "order of statuses" in the context of Spring Boot Health Indicators refers to the priority or precedence of the health statuses. When determining the overall health of the application, Spring Boot evaluates the health status of individual components and reports the most severe status encountered. Here's what the order implies:
DOWN, OUT_OF_SERVICE, UNKNOWN, UP

</details>



<details>
  <summary>How to change the Health Indicator status severity order?</summary>

1. Custom Health Indicators: Create custom health indicators to define your own health check logic (implements HealthIndicator)
2. Custom Health Aggregator: Implement a custom HealthAggregator to control how individual health statuses are aggregated into the overall health status.
</details>


<details>
  <summary>When to use @SpringBootTest annotation?</summary>

The @SpringBootTest annotation in Spring Boot is used for integration testing. It is designed to bootstrap the entire Spring application context and run tests in an environment similar to a production setup. But it's not configure web server by default.
</details>

<details>
  <summary>What does @SpringBootTest auto-configure</summary>
@SpringBootTest = @BootstrapWith(SpringBootTestContextBootstrapper.class) + @ExtendWith({SpringExtension.class})

It configures:
- loads the full Spring application context, including all beans, configurations, and properties defined in your application
- triggers all the auto-configuration classes that are typically loaded by Spring Boot when the application starts, ensuring that components such as data sources, JPA repositories, and web layers are configured
- Loads application properties from application.properties
- Ensures that all beans are properly autowired and dependencies are injected as they would be in the actual running application
- Provides a pre-configured TestRestTemplate bean for making REST calls to the embedded web server
- TestEntityManager: Offers a TestEntityManager for JPA-based tests, simplifying the setup and teardown of database state
-  If you specify a web environment (e.g., SpringBootTest.WebEnvironment.RANDOM_PORT), it starts an embedded web server
-  Allows overriding properties specifically for tests using the @TestPropertySource annotation or properties attribute of @SpringBootTest
  
</details>

<details>
  <summary>What dependencies does spring-boot-starter-test brings to the classpath?</summary>

- JUnit 5 (Jupiter)
- Spring Test
- AssertJ
- Hamcrest
- Mockito
- JSONassert
- JsonPath
- Spring Boot Test Autoconfigure
</details>


<details>
  <summary>How to perform integration testing with @SpringBootTest for a web application?</summary>

- Use webEnvironment attribute to specify the type of web environment (embedded server) to use for the tests.
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
- Use TestRestTemplate for HTTP Requests
- Verify Web Layer Behavior
- also you can configure Test Properties (Optional):
@TestPropertySource(properties = {
    "server.port=0", // Use a random port
    "spring.datasource.url=jdbc:h2:mem:testdb" // Use an in-memory database
})

</details>


<details>
  <summary>When to use @WebMvcTest? What does it auto-configure?</summary>

Use @WebMvcTest when you want to:
- Test Spring MVC components, especially controllers, in isolation from the rest of the application.
- Focus on the web layer’s behavior, including request handling and response formatting.

Auto-Configured Components:
- DispatcherServlet
- RequestMappingHandlerMapping and RequestMappingHandlerAdapter
- ExceptionHandlerExceptionResolver
- MessageConverters and ContentNegotiationManager
- MockMvc
- Jackson
</details>


<details>
  <summary>What are the differences between @MockBean and @Mock?</summary>

- @MockBean: Used in Spring Boot tests to replace beans in the Spring ApplicationContext with mocks. Automatically integrates with the Spring context.
- @Mock: Used in unit tests to create mock objects without involving the Spring context. Requires manual setup and initialization.
</details>

<details>
  <summary>When to use @DataJpaTest for? What does it auto-configure?</summary>

Use @DataJpaTest when you want to:
- Test JPA repositories and data access layers.
- Focus on database interactions and entity mappings.

Auto-Configured Components:
- In-Memory Database
- EntityManager
- Repositories: Scans and sets up Spring Data JPA repositories.
- Transaction Management: Configures transactions that are rolled back after each test.
- JPA Configuration: Provides basic JPA infrastructure for testing.
</details>


<details>
  <summary>How to customize Spring auto configuration?</summary>

- Exclude Auto-Configuration Classes: @SpringBootApplication(exclude = {DataSourceAutoConfiguration.class})
- Customize Auto-Configured Beans: You can provide your own beans that override the auto-configured beans
- Use Conditional Annotations
- Profile-Specific Configuration
- Customizing Spring Boot Starters: Define your own starter by creating a new module with a spring-boot-starter dependency and provide auto-configuration classes and meta-information in META-INF/spring.factories.
- Using spring.factories : org.springframework.boot.autoconfigure.EnableAutoConfiguration=\
com.example.MyCustomAutoConfiguration
</details>


<details>
  <summary>How to enable support for scheduled tasks in SpringBoot?</summary>

- Add @EnableScheduling	on @Configuration class. And @SpringBootApplication because it contains @Configuration inside.
- @Scheduled: Used on methods to specify the execution schedule. @Scheduled(fixedRate = 5000) // Runs every 5 seconds
</details>


<details>
  <summary>How to enable support for async operations in SpringBoot?</summary>

- Add @EnableAsync on @Configuration class. And @SpringBootApplication because it contains @Configuration inside.
- Add @Async on methods to indicate that they should be executed asynchronously. Returns: Can return void or a Future, CompletableFuture, or ListenableFuture.
</details>

<details>
  <summary>Which endpoints are exposed by default via HTTP, after adding spring-boot-starter-actuator as a dependency to your project?</summary>

- /actuator/info
- /actuator/health
</details>


<details>
  <summary>Which is the default logging system used by Spring Boot?</summary>
Logback
</details>


<details>
  <summary>Can the default script names for schema.sql and data.sql be customized?</summary>

Yes. For example if spring.datasource.platform is set to "mysql", then scripts names data-mysql.sql and schema-mysql.sql will be loaded.
</details>


<details>
  <summary>What is the correct order in which Spring Boot will look for externalized configuration - properties files?</summary>

- Application properties packaged inside your jar ( application.properties and YAML variants).
- Profile-specific application properties packaged inside your jar (application-{profile}.properties and YAML variants).
- Application properties  outside of your packaged jar (application.properties and YAML variants).
- Profile-specific application properties outside of your packaged jar (application-{profile}.properties sand YAML variants).
</details>





