<details>
  <summary>What is AOP</summary><br>
Aspect-orienting programming allows for solving cross-cutting concerns. When we have a layered application and there is some functionality 
  that cuts across the layers, like logging, security, transaction management and etc.
</details>

<details>
  <summary>What is a cross-cutting concern?</summary><br>
  Concern that cut across multiple types and objects
</details>

<details>
  <summary>What are components of AOP?</summary><br>

<ol>
    <li>aspect</li>
    <li>join point</li>
    <li>advice</li>
	<li>pointcut</li>
</ol>
</details>

<details>
  <summary>What is aspect?</summary>
  A module or class that cuts across multiple classes. 
  Example: Transaction management
</details>

<details>
  <summary>What is join point?</summary>
A point during the execution of a program where the aspect can be applied.
In Spring AOP, a join point always represents a method execution.
</details>

<details>
  <summary>What is advice?</summary>
Action taken by the aspect in a specific join point
Types: before, after, around
</details>

<details>
  <summary>What is pointcut?</summary>
  A predicate that matches join points. Advice is associated with a pointcut expression and runs at any join point matched by the pointcut 
  (for example, the execution of a method with a certain name).
</details>

<details>
  <summary>What is adviced(target) object?</summary>
  An object being advised by one or more aspects. Since Spring AOP is implemented by using runtime proxies, this object is always a proxied object.
</details>

<details>
  <summary>What is waving?</summary>
  Linking aspects with other application types or objects to create an advised object.
</details>

<details>
  <summary>What are Spring AOP types of advise</summary>
  
- Before
- After returning
- After throwing
- After (finally)
- Around - the most general kind, should not be used frequently
</details>

<details>
  <summary>Can be advised fields in Spring AOP?</summary>
  Spring AOP - Field interception is not implemented
</details>

<details>
  <summary>AspectJ vs Spring AOP?</summary>

Spring AOP:
- proxy based in runtime
- only use method-execution join points
- aspects aren't applied when calling another method within the same class
- only for beans
- runtime overhead

AspectJ AOP:
- load-time weaving - needs AspectJ Compiler
- supports all joinpoints
- aspects are applied when calling another method within the same class
- no restrictions
- less runtime overhead
</details>

<details>
  <summary>Default proxy for Spring AOP?</summary>
JDK dynamic proxy (interface based). But also can use CGLIB
</details>

<details>
  <summary>Can Spring AOP advise aspects with other aspects?</summary>
  No. Because the proxy-based mechanism.
</details>

<details>
  <summary>Simple example of Spring AOP implementation</summary>
  
  ```
  // enable AspectJ support
@Configuration
@EnableAspectJAutoProxy
public class AppConfig {
}

// declaring the aspect
@Aspect
public class NotVeryUsefulAspect {


  @Pointcut("execution(* transfer(..))") // the pointcut expression
    private void anyOldTransfer() {} // the pointcut signature
		
}
  ```
</details>

<details>
  <summary>Supported Pointcut Designators</summary>
  
- `this`
- `target`
- `args`
- `@target`
- `@args`
- `@within`
- `@annotation`
- + Spring AOP: `bean`(idOrNameOfBean)

@Pointcut("execution(public * *(..))")
	public void publicMethod() {}

@Pointcut("within(com.xyz.trading..*)")
	public void inTrading() {}

@Pointcut("publicMethod() && inTrading()")
	public void tradingOperation() {}

// The execution of any method with a name that begins with set:
@Pointcut("execution(* set*(..))")
	public void setMethod() {}

// The execution of any method defined by the AccountService interface:
@Pointcut("execution(* com.xyz.service.AccountService.*(..))")
	public void accountServiceMethod() {}

// where the argument passed at runtime is Serializable
@Pointcut("args(java.io.Serializable)")
	public void serializableParamMethod() {}

// target object has a @Transactional annotation
@Pointcut("@target(org.springframework.transaction.annotation.Transactional)")
	public void transactionalAnnotatedObjectMethod() {}

// declared type of the target object has an @Transactional annotation
@Pointcut("@within(org.springframework.transaction.annotation.Transactional)")

// executing method has an @Transactional annotation:
@Pointcut("@annotation(org.springframework.transaction.annotation.Transactional)")

// runtime type of the argument passed has the @Classified annotation:
@Pointcut("@args(com.xyz.security.Classified)")

// on a Spring bean named tradeService:
@Pointcut("bean(tradeService)")
</details>

<details>
  <summary>Spring AOP: target VS this?</summary>

// interface AccountService implements Service

// class BasicAccountService implements AccountService

// proxied by an iterface - means by AccountService

// BasicAnnotationService methods don't match
// because proxy AccountService doesn't implement AccountService
@Pointcut("this(com.xyz.service.AccountService)")
	public void accountServiceMethod() {}

// BasicAnnotationService methods match
// because proxy target BasicAnnotationService implements AccountService
@Pointcut("target(com.xyz.service.AccountService)")
	public void accountServiceMethod() {}

// this(Type) - Checks the proxy type - method of obj that impl ProxyType that impl Type 
// target(Type) - Checks the declared type - method of obj that impl Type 

</details>


<details>
  <summary>Example of Declaring advice</summary>
  
  ```
  @Aspect
public class BeforeExample {
	// 1 - inline pointcut expression
	@Before("execution(* com.xyz.dao.*.*(..))")
	public void doAccessCheck() {
		// ...
	}
	// 2 - named pointcut
	@Before("com.xyz.CommonPointcuts.dataAccessOperation()")
	public void doAccessCheck() {
		// ...
	}
}
  ```
</details>

<details>
  <summary>Passing Parameters to Advice - example</summary>

```
// 1 way of wiring
@Before("execution(* com.xyz.dao.*.*(..)) && args(account,..)")
public void validateAccount(Account account) {
	// ...
}
// 2 way of wiring - to declare a named pointcut with parameter that will 
// refer to the advice
@Pointcut("execution(* com.xyz.dao.*.*(..)) && args(account,..)")
private void accountDataAccessOperation(Account account) {}
//
@Before("accountDataAccessOperation(account)")
public void validateAccount(Account account) {
	// ...
}
```
</details>


<details>
	<summary>With what type of advice can be used JoinPoint argument?</summary>
With all
</details>

<details>
	<summary>Arguments for different methods annotated with advice</summary>

- @Before("execution(* com.example.service.*.*(..))") public void logBefore(JoinPoint joinPoint) {}
- @AfterReturning(pointcut = "execution(* com.example.service.*.*(..))", returning = "result") public void logAfterReturning(JoinPoint joinPoint, Object result) {}
- @AfterThrowing(pointcut = "execution(* com.example.service.*.*(..))", throwing = "ex") public void logAfterThrowing(JoinPoint joinPoint, Throwable ex) {}
- @After("execution(* com.example.service.*.*(..))") public void logAfter(JoinPoint joinPoint) {}
- @Around("execution(* com.example.service.*.*(..))") public Object around(ProceedingJoinPoint joinPoint) throws Throwable {}

JoinPoint provides:
- Method Signature: Get the name, return type, and parameter types of the method.
- Method Arguments: Access and modify the arguments passed to the method.
- Target Object: Access the object on which the method is being invoked.

ProceedingJoinPoint provides the same + Object result = proceedingJoinPoint.proceed(args);
</details>


<details>
	<summary>What features are available out of the box by Spring Boot actuator?</summary>

- /actuator/health
- /actuator/metrics
- /actuator/env
- /actuator/info
- /actuator/threaddump
- /actuator/loggers
- /actuator/auditevents
- /actuator/prometheus: (If the micrometer-registry-prometheus dependency is included)
- /actuator/httptrace
- /actuator/shutdown: (If enabled) Allows you to gracefully shut down the application via a POST request. This endpoint must be explicitly enabled due to its potentially disruptive nature.
</details>
