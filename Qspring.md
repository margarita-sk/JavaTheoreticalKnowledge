Container, Dependency and IOC
• What is dependency injection and what are the advantages of using it?
• What is an interface and what are the advantages of making use of them in Java?
• What is an ApplicationContext?
• How are you going to create a new instance of an ApplicationContext?
• Can you describe the lifecycle of a Spring Bean in an ApplicationContext?
• How are you going to create an ApplicationContext in an integration test?
• What is the preferred way to close an application context? Does Spring Boot do this for
you?
• Can you describe:
– Dependency injection using Java configuration?
– Dependency injection using annotations (@Autowired)?
– Component scanning, Stereotypes?
– Scopes for Spring beans? What is the default scope?
• Are beans lazily or eagerly instantiated by default? How do you alter this behavior?
– What is an initialization method and how is it declared on a Spring bean?
– What is a destroy method, how is it declared and when is it called?
– Consider how you enable JSR-250 annotations like @PostConstruct and @PreDestroy?
When/how will they get called?
– How else can you define an initialization or destruction method for a Spring bean?
• What does component-scanning do?
• What is the behavior of the annotation @Autowired with regards to field injection,
constructor injection and method injection?
• How does the @Qualifier annotation complement the use of @Autowired?
• What is a proxy object and what are the two different types of proxies Spring can create?
– What are the limitations of these proxies (per type)?
– What is the power of a proxy object and where are the disadvantages?

• What does the @Bean annotation do?
• What is the default bean id if you only use @Bean? How can you override this?
• Why are you not allowed to annotate a final class with @Configuration
– How do @Configuration annotated classes support singleton beans?
– Why can’t @Bean methods be final either?
• How do you configure profiles? What are possible use cases where they might be useful?
• Can you use @Bean together with @Profile?
• Can you use @Component together with @Profile?
• How many profiles can you have?
• How do you inject scalar/literal values into Spring beans?
– What is @Value used for?
• What is Spring Expression Language (SpEL for short)?
• What is the Environment abstraction in Spring?
• Where can properties in the environment come from – there are many sources for
properties – check the documentation if not sure. Spring Boot adds even more.
• What can you reference using SpEL?
• What is the difference between $ and # in @Value expressions?

• What is the @Controller annotation used for?
• How is an incoming request mapped to a controller and mapped to a method?
• What is the difference between @RequestMapping and @GetMapping?
• What is @RequestParam used for?
• What are the differences between @RequestParam and @PathVariable?
• What are the ready-to-use argument types you can use in a controller method?
• What are some of the valid return types of a controller method?

What does REST stand for?
• What is a resource?
• Is REST secure? What can you do to secure it?
• Is REST scalable and/or interoperable?
• Which HTTP methods does REST use?
• What is an HttpMessageConverter?
• Is @Controller a stereotype? Is @RestController a stereotype?
– What is a stereotype annotation? What does that mean?
• What is the difference between @Controller and @RestController?
• When do you need to use @ResponseBody?
• What are the HTTP status return codes for a successful GET, POST, PUT or DELETE
operation?
• When do you need to use @ResponseStatus?
• Where do you need to use @ResponseBody? What about @RequestBody?
• If you saw example Controller code, would you understand what it is doing? Could you
tell if it was annotated correctly?

• What are authentication and authorization? Which must come first?
• Is security a cross cutting concern? How is it implemented internally?
• What is the delegating filter proxy?
• What is the security filter chain?
• What is a security context?
• What does the ** pattern in an antMatcher or mvcMatcher do?
• Why is the usage of mvcMatcher recommended over antMatcher?
• Does Spring Security support password encoding?
• Why do you need method security? What type of object is typically secured at the
method level (think of its purpose not its Java type).
• What do @PreAuthorized and @RolesAllowed do? What is the difference between them?
• How are these annotations implemented?
• In which security annotation, are you allowed to use SpEL?

What is Spring Boot?
• What are the advantages of using Spring Boot?
• What things affect what Spring Boot sets up?
• What is a Spring Boot starter? Why is it useful?
• Spring Boot supports both properties and YML files. Would you recognize and
understand them if you saw them?
• Can you control logging with Spring Boot? How?
• Where does Spring Boot look for application.properties file by default?
• How do you define profile specific property files?
• How do you access the properties defined in the property files?
• What properties do you have to define in order to configure external MySQL?
• How do you configure default schema and initial data?
• What is a fat jar? How is it different from the original jar?
• What embedded containers does Spring Boot support? 

What value does Spring Boot Actuator provide?
• What are the two protocols you can use to access actuator endpoints?
• What are the actuator endpoints that are provided out of the box?

When do you want to use @SpringBootTest annotation?
• What does @SpringBootTest auto-configure?
• What dependencies does spring-boot-starter-test brings to the classpath?
• How do you perform integration testing with @SpringBootTest for a web application?
• When do you want to use @WebMvcTest? What does it auto-configure?
• What are the differences between @MockBean and @Mock?
• When do you want @DataJpaTest for? What does it auto-configure?
