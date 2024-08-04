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
