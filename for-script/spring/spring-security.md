<details>
  <summary>What is FilterChainProxy?</summary>

It's a class that delegates Filter requests to a list of Spring-managed filter beans.
As of version 2.0, you shouldn't need to explicitly configure a FilterChainProxy bean in your application context unless you need very 
fine control over the filter chain contents. Most cases should be adequately covered by the default <security:http /> namespace configuration options.
</details>

<details>
  <summary>What is DelegatingFilterProxy?</summary>

It's a class that acts as a proxy for a standard Servlet Filter, delegating to a Spring-managed bean that implements the Filter interface
</details>

<details>
  <summary>What is SecurityContextHolder?</summary>

It's a class that associates a given SecurityContext  with the current execution thread
</details>
