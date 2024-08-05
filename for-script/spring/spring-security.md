<details>
  <summary>What is DelegatingFilterProxy?</summary>
  
The Servlet container allows registering Filter instances using its own standards, but it is unaware of Spring-defined Beans. 

- DelegatingFilterProxy on the one hand is just a Filter so it can be registered through the standard Servlet container mechanisms. 
- on the other hand, DelegatingFilterProxy is a Spring implementation that looks up Bean filter from the ApplicationContext.
- it's an extension of GenericFilterBean (in Spring Boot it is registered by DelegatingFilterProxyRegistrationBean)
- it's a bridge between the Servlet container’s lifecycle and Spring’s ApplicationContext.
</details>


<details>
  <summary>What is FilterChainProxy?</summary>

- bean filter provided by Spring Security that allows delegating a request to a specific SecurityFilterChain.
- it is wrapped in a DelegatingFilterProxy.
</details>


<details>
  <summary>What is SecurityFilterChain?</summary>

SecurityFilterChain is used by FilterChainProxy to determine which Spring Security Filter instances should be invoked for the current request.
</details>


<details>
  <summary>Name Spring security filters</summary>

- CsrfFilter
- UsernamePasswordAuthenticationFilter
- BasicAuthenticationFilter
- AuthorizationFilter
- ExceptionTranslationFilter
</details>


<details>
  <summary>What is SecurityContext?</summary>
SecurityContext contains an Authentication object.

Authentication object:
- is an input to AuthenticationManager to provide the credentials a user has provided to authenticate.
- Represent the currently authenticated user. You can obtain the current Authentication from the SecurityContext.
</details>


<details>
  <summary>What is SecurityContextHolder?</summary>

It's a class that associates a given SecurityContext  with the current execution thread
</details>



<details>
  <summary>Name Authentication Mechanisms in Spring</summary>

- Basic Authentication
- OAuth 2.0 - SSO protocol
- SAML 2.0 (Security Assertion Markup Language 2.0) - SSO protocol
- Central Authentication Server (CAS) is a single sign-on (SSO) protocol
- Remember-Me Authentication
- JAAS Authentication - authenticate with JAAS
- Pre-Authentication Scenarios - authenticate with an external mechanism such as SiteMinder or Java EE security but still use Spring Security
- X509 Authentication
</details>


<details>
  <summary>What does the ** pattern in an antMatcher or mvcMatcher do?</summary>

In Spring Security, the ** pattern used in antMatcher or mvcMatcher is a wildcard pattern that matches multiple levels of directories or path segments.
-  match zero or more directories in the URL path.
</details>


<details>
  <summary>Name the patterns used in antMatcher or mvcMatcher</summary>

- \* (Single Level Wildcard) Matches: A single path segment
- \** (Multi-Level Wildcard) Matches: Zero or more path segments.
- ? (Single Character Wildcard) Matches: A single character.
- {} (Path Variable) Matches: Used to denote path variables in URL patterns, particularly in Spring MVC.
- \[ \] (Character Class) Matches: One character from a set of characters. This is less commonly used in Spring and more familiar in regex. Example: /files/\[a-zA-Z0-9\]*.txt: Matches files like /files/file1.txt
- Regular Expressions Matches: Custom patterns using regular expressions (more advanced and less common in antMatcher or mvcMatcher directly but possible through custom configurations).
</details>


<details>
  <summary>What is recommended to use: mvcMatcher or antMatcher?</summary>

  Generally, mvcMatcher is more secure than an antMatcher. As an example:

- antMatchers("/secured") matches only the exact /secured URL
- mvcMatchers("/secured") matches /secured as well as /secured/, /secured.html, /secured.xyz 
</details>






<details>
  <summary>What annotations will be enabled by the usage of @EnableGlobalMethodSecurity(jsr250Enabled = true) </summary>

- @RolesAllowed: Restricts access to methods based on user roles.
- @PermitAll: Allows all users to access the method.
- @DenyAll: Denies access to all users.
- @DeclareRoles: Declares security roles within the application.
</details>




<details>
<summary>Explain OAuth 2.0</summary>
</details>

<details>
<summary>Explain SAML 2.0</summary>
</details>

<details>
  <summary>What is SSO protocol? What are implementation of SSO?</summary>
</details>

<details>
  <summary>What is JAAS?</summary>
</details>

