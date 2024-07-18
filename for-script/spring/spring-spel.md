<details>
  <summary>Where does SpEL can be used?</summary>

1. Spring XML Configuration
```
<bean id="exampleBean" class="com.example.ExampleBean">
    <property name="name" value="#{systemProperties['user.name']}" />
    <property name="currentDate" value="#{new java.util.Date()}" />
</bean>
```
2. Annotations

- @Value("#{systemProperties['user.name']}")
- @ConditionalOnExpression("#{systemProperties['os.name'].toLowerCase().contains('win')}")
- @Scheduled(cron = "#{@myCronExpression}")

3. Spring Security
@PreAuthorize("hasRole('ROLE_ADMIN')")
@PreAuthorize("#username == authentication.name")

4. Spring Data - Repository Query Methods
@Query("SELECT u FROM User u WHERE u.name = :#{#name}")

5. Spring Boot application properties
my.custom.property=#{systemProperties['user.home']}/myapp

6. Testing - Spring TestContext Framework
@WithUserDetails(value = "#{testUser.username}")

and others
</details>

<details>
  <summary>What literals does SpEL support?</summary>

SpEL supports the following types of literal expressions:
- strings
- numeric values: integer (`int` or `long`), hexadecimal (`int` or `long`), real (`float` or `double`)
- boolean values: `true` or `false`
- null
</details>

<details>
  <summary>What relation operators supports SpEL?</summary>
    
    ```
    // evaluates to true
    boolean trueValue = parser.parseExpression("'black' < 'block'").getValue(Boolean.class);
    
    // uses CustomValue:::compareTo
    boolean trueValue = parser.parseExpression("new CustomValue(1) < new CustomValue(2)").getValue(Boolean.class);
    
    // null is treated as nothing (that is NOT as zero). 
    // As a consequence, any other value is always greater than null 
    
    // evaluates to false
    boolean falseValue = parser.parseExpression("'xyz' instanceof T(Integer)").getValue(Boolean.class);
    
    // evaluates to true
    boolean trueValue = parser.parseExpression("'5.00' matches '^-?\\d+(\\.\\d{2})?$'").getValue(Boolean.class);
    ```
    
    Each symbolic operator can also be specified as a purely alphabetic equivalent:
    
    - `lt` (`<`)
    - `gt` (`>`)
    - `not` (`!`)
    - etc.
</details>
