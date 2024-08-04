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
<summary>What operators can be used with SpEL?</summary>

  - Relation operators:  `lt` (`<`), `gt` (`>`), `not` (`!`)
  - Logical Operators: `and` (`&&`), `or` (`||`), `not` (`!`)
  - Ternary Operator: "isMember(#queryName)? 'is a member' : #queryName + ' is not a member'"
  - Elvis operator: "#{systemProperties['pop3.port'] ?: 25}"

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

<details>
  <summary>How to define in SpEL: type, constructor, bean references, collection selection</summary>

- Type: ``"T(java.util.Date)"``
- Constructor: ``"new org.spring.samples.spel.inventor.Inventor('Albert Einstein', 'German')"``
- Bean from the application context: ``"@SomeBean"``
- Bean from
- Collection: ``"members.?[nationality == 'Serbian']"`` of ``"map.?[value<27]"``
</details>


<details>
  <summary>What is the default SpEL Compiler mode?</summary>
OFF.

Even when the SpEL compiler is disabled, Spring can still evaluate SpEL expressions interpretively instead of compiling them into bytecode.
In Interpretation mode: Spring parses the SpEL expression into an abstract syntax tree (AST). The parsed expression tree is then evaluated at runtime. Spring traverses the AST and interprets each node to produce the final value.

While interpretive evaluation is slightly slower than compiled evaluation due to the overhead of interpreting the AST at runtime, it is still effective and correct. The difference is mostly noticeable in scenarios with a high volume of SpEL evaluations.

</details>

<details>
  <summary>How can we configure SpEL compiler mode?</summary>

- through spring.expression.compiler.mode, by setting the value to be one of the SpelCompilerMode enum - OFF, IMMEDIATE or MIXED
- if we use SpEL through ExpressionParser, we can use SpelCompilerConfiguration class as well to manipulate the compilers mode.
</details>

