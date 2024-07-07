<details>
  <summary>What is Spring?</summary>
Spring is a framework for building Java applications that contains a lot of different modules that can be added or not depending on needs. 
The key feature of the Spring framework is the inversion of control.
</details>

<details>
  <summary>What are Spring modules?</summary>
  
  - Spring Core container
  - Spring AOP
  - Spring Web
  - Spring Test
  - Spring Security, etc.
</details>


<details>
  <summary>What is Inversion of Control?</summary>
  It is the design principle when the dependent part is not responsible for creating and managing its dependencies. 
</details>

<details>
  <summary>What is Dependency Injection?</summary>
  DI is a form of IoC when an IoC container injects dependencies into dependent parts.
</details>

<details>
  <summary>What is Dependency Lookup?</summary>
  It's a form of IoC when the dependent part looks for dependencies.
</details>

<details>
  <summary>Advantages and Disadvantages of Dependency Injection</summary>
  
  Advantages:
  - low coupling
  - reusability of code
  - readability and maintainability
  - easy testing
    
  Disadvantages:
  - increase complexity, especially in small apps
  - runtime errors
</details>

<details>
  <summary>BeanFacory vs ApplicationContext</summary>

  | |BeanFactory|ApplicationContext|
  |-----|-----|----|
  | | simplest container providing DI support| implements BeanFactory and adds more features|
  |bean initialization | lazy | by default eager | 
  | when to use | lightweight apps where memory consumption is critical | all other cases | 
  | event propogation| no | supports |
  | BeanFactoryPostProcessor | no automatic registration | automatic registration |
  | BeanPostProcessor | no automatic registration | automatic registration |
  | message resource handling| no | yes |
  | internationalization| no | yes |
</details>

<details>
  <summary>What is the ApplicationContext?</summary>
  Interface that represents IoC container and is responsible for bean management.
</details>

<details>
  <summary>What is a Bean?</summary>
  Object that is handled by Spring IoC container
</details>

<details>
  <summary>Can @Bean annotated methods be static?</summary>
  Yes, but they won't participate in the bean lifecycle as normal beans. They will be created before bean instantiation and without a proxy mechanism. 
  It can be useful if we would like to create BeanFactoryPostProcessor and BeanPostProcessor beans.
</details>

<details>
  <summary>Can @Bean methods be final?</summary>
  No, it will cause a compilation error.
</details>

<details>
  <summary>How ApplicationContext define which objects to instantiate, configure, and assemble?</summary>
BeanDefinitionReader reads configuration metadata: 1 XML, 2 Java annotations, 3 Java code and creates BeanDefinitions. Based on them beans are 
  instantiated and configured (scope, dependencies, other configuration settings)
</details>

<details>
  <summary>Dependency Injection mechanisms</summary>

  1. Constructor DI
  2. Setter DI
  3. Field DI (reflection)
</details>

<details>
  <summary>Can the collection be injected?</summary>
  Yes, but the qualifier should be specified.
  ```
  @Service
public class CollectionInjection {
    @Autowired
    @Qualifier("map")
    private Map<String, Object> map;
}
  ```
</details>

<details>
  <summary>Constructor-based or setter-based DI or field DI?</summary>
  
  ||constructor-based DI| setter-based DI | field DI |
  |---|---|---|---|
  |when|during instantiation | during initialization | during initialization|
  |no dependency in IoC container| throws NoSuchBeanDefinitionException | dependency can be null | dependency can be null|
  |usecase| for mandatory dependencies | for optional dependencies | for optional dependencies |
  |testing| easy  | easy  | harder |
</details>

<details>
  <summary>When beans are created?</summary>
  Singleton scoped beans are created during the container creation, others - when they are requested.
</details>

<details>
  <summary>When circular dependency may appear?</summary>
  When using a constructor or field injection class A requires class B in the constructor and class B requires class A when the app startup appears
  
  ``The dependencies of some of the beans in the application context form a cycle: ...``
</details>

<details>
  <summary>What is Lookup Method Injection?</summary>
  It is a feature in the Spring Framework that allows a bean to override the lookup method to get a new instance of a dependency whenever the method is called. This is particularly useful in scenarios where you want to obtain a new instance of a prototype-scoped bean within a singleton-scoped bean.

  ```
@Component
@Scope("prototype")
public class MyPrototypeBean {
    // Prototype bean implementation
}


import org.springframework.beans.factory.annotation.Lookup;
import org.springframework.stereotype.Component;

@Component
public class MySingletonBean {

    // This method will be overridden by Spring to provide a new instance of MyPrototypeBean
    @Lookup
    public MyPrototypeBean getPrototypeBean() {
        return null; // The actual implementation is generated by Spring at runtime
    }

    public void doSomething() {
        // Obtain a new instance of MyPrototypeBean through the lookup method
        MyPrototypeBean prototypeBean = getPrototypeBean();
        
        // Use the prototype bean
        // ...
    }
}
```
</details>

<details>
  <summary>What are bean scopes?</summary>

  - singleton - is created when the application context is created
  - prototype - one instance every time a request for that specific bean is made
  - session - one instance per one HTTP request
  - request - one instance per one HTTP session
  - application - one instance per one lifecycle of ServletContext 
  - websocket - one instance per one lifecycle of WebSocket
+ you can configure your own scope, or register SimpleThreadScope(it exists but is not registered)
</details>

<details>
  <summary>How to handle Singleton Beans with Prototype-bean Dependencies?</summary>
  Lookup method injection
</details>

<details>
  <summary>What is the difference between bean id, alias, and bean qualifier?</summary>
The ID is a unique identifier - it can be only one. There can be a lot of aliases as well as qualifiers.
  
  ```
  @Component
public class Singer { } //id=singer, aliases=

@Component("johnMayer")
public class Singer { } //id=johnMayer, aliases=

@Configuration
public class Config {

	@Bean(name={"john", "johnny"}) //id=singer, aliases=["john", "johnny"]
  public Singer singer(){
	  return new Singer();
	}

	@Bean //id=johnMayer
  public Singer johnMayer(){
	  return new Singer();
	}
}
  ```
If we have more than one bean that qualifies for spring injection, then we use `@Qualifer` to specify which needs to be used for injection.

There **is** a difference: `@Bean("simpleCar")` (or `@Component("car")`) gives your bean with name "car" in the Spring Context, whereas `@Qualifier("car")` only adds information **without changing the name of the bean**.

```
@Configuration
public class Config {
    @Bean("car")
    public Vehicle car(){ return ...}
}

@Component("car")
public class MuscleCar implement Vehicle {...}

@Component
@Qualifier("car")
public class ElectroCar implement Vehicle {...}


public class DriveService {

    private final Vehicle vehicle;

    @Autowired
    public Driver(@Qualifier("car") Vehicle vehicle) {
      this.vehicle = vehicle;
    }
}


@Component
@Qualifier("beanQualifier")
class BeanTwo implements TypeOne { }

@Component
@Qualifier("beanQualifier")
class BeanThree implements TypeOne { }

@Autowired
@Qualifier("beanQualifier")
Map<String, TypeOne> typeOneMap;
// The map will only contain the 2 beans with the qualifier "beanQualifier".
// {beanThree=BeanThree@9f674ac, beanTwo=BeanTwo@1da4b3f9}
```

</details>

<details>
  <summary></summary>
</details>
