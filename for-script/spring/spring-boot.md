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


</details>

@EnableScheduling	
@EnableAsync	

@EventListener	







