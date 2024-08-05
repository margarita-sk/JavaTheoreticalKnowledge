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
  <summary>Does Spring Security support password hashing</summary>

Yes. Password hashing is a process of transforming a plain-text password into a hashed value using a cryptographic hash function. Spring Security provides built-in support for password hashing through various PasswordEncoder implementations. Some common implementations include:
- BCryptPasswordEncoder
- PBKDF2PasswordEncoder: Uses the PBKDF2 (Password-Based Key Derivation Function 2) algorithm, which applies a cryptographic hash function multiple times.
- SCryptPasswordEncoder
- NoOpPasswordEncoder: For cases where no encoding is applied (not recommended for production use).
</details>


<details>
  <summary>What is Salting in a security context and how does Spring handle it?</summary>

  Salting involves adding a random value (called a "salt") to the password before hashing it. This random value is unique for each password and ensures that even if two users have the same password, their hashed values will be different due to different salts.

Spring Security implementations like BCryptPasswordEncoder, PBKDF2PasswordEncoder, and SCryptPasswordEncoder handle salting automatically, providing robust protection against password-cracking attacks.
</details>


<details>
  <summary>How method-security is enabled in Spring?</summary>

@EnableGlobalMethodSecurity(prePostEnabled = true, securedEnabled = true, jsr250Enabled = true):
- prePostEnabled = true: Enables Spring Security pre/post annotations (@PreAuthorize, @PostAuthorize).
- securedEnabled = true: Enables the use of the @Secured annotation.
- jsr250Enabled = true: Enables the use of JSR-250 annotations like @RolesAllowed.
</details>

<details>
  <summary>Name security levels in Spring Security and how they are implemented</summary>

- URL Level Security: antMatchers(), mvcMatchers()
- Method Level Security: prePost, secured, jsr250
</details>


<details>
  <summary>Name and explain prePost security annotations in Spring</summary>
way to secure methods and classes
  
- @PreAuthorize: specify a condition that must be met before a method is invoked, uses Spring Expression Language (SpEL): @PreAuthorize("hasRole('ROLE_USER') and #user.id == principal.id")
- @PostAuthorize: @PostAuthorize("returnObject.owner == authentication.principal.username")
</details>


<details>
  <summary>Explain @Secured annotation in Spring</summary>

  @Secured - method level annotation, is used to specify a list of roles that are allowed to invoke a method: @Secured({"ROLE_USER", "ROLE_ADMIN"})
</details>


<details>
  <summary>Name and explain JSR-250 security annotations in Spring</summary>
way to secure methods and classes using role-based access control
  
- @RolesAllowed: @RolesAllowed({"ROLE_USER", "ROLE_ADMIN"})
- @PermitAll: method or class is accessible to all users, regardless of their roles
- @DenyAll: a method or class is not accessible to any users. This can be useful for methods that are deprecated or under development and should not be accessible
</details>


<details>
  <summary>What is the difference between @PreAuthorise("hasRole('ROLE_USER')") and @RolesAllowed("ROLE_USER")?</summary>

- both annotations can achieve similar results for simple role-based access control
- @PreAuthorize offers more flexibility and functionality. If you need to incorporate complex security logic or conditions, @PreAuthorize is the better choice. For straightforward role checks, @RolesAllowed can be simpler and sufficient.
- @PreAuthorize: Requires enabling global method security in Spring with @EnableGlobalMethodSecurity(prePostEnabled = true).
- @RolesAllowed: Supported by default in Spring Security without additional configuration, provided the JSR-250 annotations are enabled.

</details>


<details>
  <summary>What annotations will be enabled by the usage of @EnableGlobalMethodSecurity(jsr250Enabled = true) </summary>

- @RolesAllowed: Restricts access to methods based on user roles.
- @PermitAll: Allows all users to access the method.
- @DenyAll: Denies access to all users.
- @DeclareRoles: Declares security roles within the application.
</details>





