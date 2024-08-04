<details>
  <summary>What is REST protocol?</summary>

Representational State Transfer protocol.
Architectural style and set of principles for designing networked applications, primarily used for creating web services:
- stateless
- supports different formats like JSON, XML, etc.
- Client-Server Architecture
- Uniform Interface: Resources are identified by URIs, Clients interact with resources by using representations (JSON, XML, etc.)
</details>

<details>
  <summary>What is RESTful web service?</summary>

A RESTful web service is a web service implemented using HTTP and REST principles.
The common HTTP methods used in RESTful services include: GET, POST, PUT, DELETE, PATCH.
</details>


<details>
  <summary>What is a resource in scope of REST?</summary>
  In the scope of REST (Representational State Transfer), a resource is a fundamental concept that represents any entity or object that can be identified, accessed, and manipulated through the web. 
</details>

<details>
  <summary>Is REST secure?</summary>
No. 
</details>

<details>
  <summary>Strategies to Secure RESTful APIs</summary>

  - Use HTTPS
  - Authentication
  - Authorization
  - Input Validation and Sanitization
  - Rate Limiting and Throttling
  - CORS (Cross-Origin Resource Sharing)
  - Data Encryption
  - CSRF (Cross-Site Request Forgery) Protection
  - Security Headers
  - API Gateway and Firewall
  - Security Best Practices for Development
</details>

<details>
  <summary>Is REST scalable and/or interoperable?</summary>

- REST is scalable because it is stateless, supports layered architectures, and allows for caching, which collectively facilitate the horizontal scaling of services.
- REST is interoperable due to its use of standard HTTP methods, support for multiple media types, and the principle of HATEOAS, which promotes discoverability and interaction flexibility.
</details>

<details>
  <summary>What is idempotency?</summary>
Idempotency is a key concept in web services, including RESTful APIs, and it plays a crucial role in ensuring reliable and predictable interactions between clients and servers.
Idempotency refers to the property of an operation where performing the same action multiple times has the same effect as performing it once. In other words, an operation is idempotent if repeating it does not produce a different result or side effect than the initial application.

- Idempotent: GET, PUT, DELETE
- Not Idempotent: POST
</details>

<details>
  <summary>What is an HttpMessageConverter?</summary>
mechanism for converting HTTP request and response bodies to and from Java objects. It plays a crucial role in the process of data serialization and deserialization, enabling Spring applications to handle different types of data formats (e.g., JSON, XML) in a flexible and customizable way.

  Spring provides several built-in HttpMessageConverter implementations for common data formats:
  - JSON, XML
  - Form Data:  Converts form data (key-value pairs) to and from Java objects.
  - StringHttpMessageConverter, ByteArrayHttpMessageConverter
</details>

<details>
  <summary>@RequestBody vs @ResponseBody?</summary>
  
- Use @ResponseBody when you want to directly return data from a controller method to the HTTP response body, particularly in RESTful services or when returning data formats like JSON or XML.
- Use @RequestBody when you need to map the HTTP request body to a Java object, allowing you to process data sent by the client in a structured form.
</details>

<details>
  <summary>What is @ResponseStatus?</summary>

  @ResponseStatus is used to:
  - Set HTTP status codes for exceptions to standardize error responses.
  - Customize the HTTP status code returned by specific controller methods to accurately reflect the outcome of an operation.
</details>

<details>
  <summary>What is RestTemplate?</summary>

synchronous client provided by Spring for making HTTP requests.
 While RestTemplate is deprecated in favor of WebClient in Spring 5, it remains widely used in existing applications.

</details>
