<details>
  <summary>What does @MockBean annotation do?</summary>
@MockBean creates and injects a Mockito mock into the Application Context
</details>

<details>
  <summary>What is the default value for the "webEnvironment" attribute of @SpringBootTest when a web environment is on your classpath?</summary>
MOCK
</details>

<details>
  <summary>JUnit 4 annotations</summary>
  
- @Test
- @Before - before each test method in the class
- @After
- @BeforeClass - static method that will be run once before any of the test methods
- @AfterClass
- @Ignore
- @RunWith
- @Rule
</details>


<details>
  <summary>JUnit 5 annotations</summary>
  
- @Test
- @BeforeEach - before each test method in the class
- @AfterEach
- @BeforeAll - static method to be executed once before all test methods in the current class
- @AfterAll
- @Disabled
- @Tag - to filter tests by tags
- @DisplayName
- @ParameterizedTest + @ValueSource(strings = {"Hello", "JUnit"})
- @ExtendWith
</details>

<details>
  <summary>What type of tests can be implemented with Spring?</summary>

- unit tests
- integration tests
- End-to-End Tests
- Acceptance Tests with Cucumber 
- Performance Tests with Gatling
</details>

<details>
  <summary>How can you create a shared application context in a JUnit integration test?</summary>

- @SpringBootTest: Creates a shared application context for all test methods in the class by default.
- @ContextConfiguration: Allows specifying custom configuration for the application context.
- @DirtiesContext: Marks the context as dirty and optionally refreshes it after the test class or method execution.
- @TestExecutionListeners: Provides advanced control over the test execution lifecycle, including application context management.
</details>

<details>
  <summary>@ContextConfiguration vs @TestConfiguration?</summary>

@ContextConfiguration: 
- Used to specify the configuration classes or XML files for setting up the ApplicationContext in a test.
- Applied to the test class level.
- Ideal for defining or overriding context configuration.

@TestConfiguration is a specialized form of @Configuration that is used specifically for defining beans that are used in tests. It is often used within a test class or test configuration class to provide test-specific beans or override existing beans.

@TestConfiguration:
- Used to provide additional configuration or override beans specifically for testing.
- Applied to a @Configuration class within the test class.
- Ideal for defining test-specific beans or configurations.
</details>

<details>
  <summary>How not to rollback transactions in tests?</summary>

- @Rollback(false)
- @Commit
- @Transactional(propagation = Propagation.NOT_SUPPORTED) to ensure that no transaction is started.
</details>

<details>
  <summary>Name and explain Spring Boot testing annotations</summary>

- @SpringBootTest: Loads the full application context for integration tests. It provides a comprehensive testing environment that includes all beans and configurations. Attributes: webEnvironment (e.g., MOCK, RANDOM_PORT, DEFINED_PORT, NONE).
- @DataJpaTest: Configures an in-memory database and scans for JPA repositories. It is used for testing JPA repositories and data access layers. Attributes: includeFilters and excludeFilters
- @WebMvcTest: Configures only the web layer and scans for controllers, @ControllerAdvice, and other web-related components. Arguments: controllers, excludeAutoConfiguration
- @MockBean:  Creates and injects mock beans into the application context for use in tests.
- @TestConfiguration: Defines additional configuration for tests. It is used to provide test-specific beans and configurations.
</details>

<details>
  <summary>What does @SpringBootTest do?</summary>

- @SpringBootTest is used for integration testing in a Spring Boot application. It sets up the entire application context and provides a fully initialized Spring environment to test your application’s functionality as a whole.
- When @SpringBootTest is used, it typically looks for a class annotated with @SpringBootApplication to bootstrap the application context. It uses the configuration, component scanning, and auto-configuration provided by @SpringBootApplication to set up the context for testing.
- @SpringBootConfiguration can be used in place of @SpringBootApplication for testing if you need a specific configuration for tests. It allows you to provide additional or alternative configuration without affecting the main application configuration.
</details>


