<details>
  <summary>What embedded containers are supported by Spring Boot?</summary>

  - Apache Tomcat
  - Jetty
  - Undertow
</details>

<details>
  <summary>What is MVC?</summary>

MVC stands for Model-View-Controller. It is a design pattern used in software development to separate concerns and organize code in a way that improves maintainability and scalability. The idea behind MVC is to divide an application into three interconnected components:
- Model: In a Java web application, the model might be a class representing a Person with properties such as name and age, and methods to access and update this data.
- View: In a web application, this could be an HTML page or a JavaScript component that presents a form to the user to input and view data.
- Controller: In a web application, the controller might be a servlet or a class with methods that handle HTTP requests, interact with the model, and decide which view to display to the user.
</details>

<details>
  <summary>What is the DispatcherServlet in Spring?</summary>

DispatcherServlet is a central servlet in Spring MVC that handles incoming HTTP requests and routes them to the appropriate components in the application.
It is configured in the web application's web.xml file or via Java configuration in Spring Boot applications and acts as the front controller for the Spring MVC framework.

Responsibilities:
- Receives all incoming HTTP requests and routes them to the appropriate handler methods (controllers) based on URL patterns.
- Uses HandlerMapping beans to determine the correct handler method for the incoming request.
- Binds request parameters to model attributes and prepares the data required by the view.
- Uses ViewResolver beans to select the appropriate view (e.g., JSP, Thymeleaf, etc.) for rendering the response based on the view name returned by the controller.
- Forwards the request and model data to the selected view for rendering. The view then generates the final HTML or other content to be sent back to the client.
- Handles exceptions thrown by controllers or other application parts by delegating to an appropriate ExceptionHandler or error view.
</details>

<details>
  <summary>What is a web application context in Spring? What extra scopes does it offer?</summary>

WebApplicationContext is a specialized extension of the ApplicationContext that is tailored for web applications:
- WebApplicationContext is tied to the ServletContext of a web application, allowing it to interact with and configure servlets, filters, and listeners.
- For many applications, having a single WebApplicationContext is simple and suffices.

In addition to the standard bean scopes available in the ApplicationContext, the WebApplicationContext offers additional scopes specifically for web applications:
- request scope are created once per HTTP request
- session scope are created once per HTTP session.
- application scope are created once per ServletContext
- websocket scope are created per WebSocket session
</details>


<details>
  <summary>What are @Controller and @RestController annotations?</summary>

- @Controller - @Component + presentation layer + request mapping (dispatcher scans the annotated classes and detects methods annotated)
- @RestController - @Component + @Controller + @ResponseBody + can return JSON
</details>

<details>
  <summary>How is an incoming request mapped to a controller and mapped to a method?</summary>

- Component Scanning: Spring scans for classes annotated with @Controller (or @RestController) and registers them as beans.
- DispatcherServlet: This front controller receives all HTTP requests and delegates them to a HandlerMapping.
- Handler Mapping: The HandlerMapping determines the appropriate controller and method based on request URL and HTTP method using @RequestMapping, @GetMapping, etc.
- Method Execution: The selected controller method is invoked, with parameters bound from the request using annotations like @RequestParam, @PathVariable, or @RequestBody.
</details>

<details>
  <summary>What is the difference between @RequestMapping and @GetMapping?</summary>

@GetMapping is a shortcut of @RequestMapping(method = RequestMethod.GET)
</details>

<details>
  <summary>What are the differences between @RequestParam and @PathVariable?</summary>

- @RequestParam maps query parameter: ?param=smth
- @PathVariable maps part of the path: /{pVariable}/smth

</details>


<details>
  <summary>Name URL patterns that can be used for @RequestMapping methods mapping</summary>

- PathPattern — Designed for web use, this solution deals effectively with encoding and path parameters, and matches efficiently. Is the recommended solution for web applications and it is the only choice in Spring WebFlux. Allows for optional segments, regex-like constraints, and better variable extraction
- AntPathMatcher — match String patterns against a String path. This is the original solution also used in Spring configuration to select resources on the classpath, on the filesystem, and other locations. It is less efficient and the String path input is a challenge for dealing effectively with encoding and other issues with URLs. /files/*, /files/**.
</details>


<details>
  <summary>What are the parameter types for a controller method?</summary>

- WebRequest, NativeWebRequest
- ServletRequest, HttpServletRequest, or Spring’s MultipartRequest, MultipartHttpServletRequest.
- HttpSession
- PushBuilder
- Principal
- HttpMethod
- Locale, TimeZone, ZoneId
- InputStream, Reader
- OutputStream, Writer
- @PathVariable, @MatrixVariable, @RequestParam, @RequestHeader, @CookieValue, @RequestBody, @RequestPart
- HttpEntity<B>
- Map, Model, ModelMap
- Errors, BindingResult
- @SessionAttributes
- and others
</details>



<details>
  <summary>What annotations might you use on a controller method parameter?</summary>

- @RequestParam: For query parameters.
- @PathVariable: For URL path variables.
- @RequestBody: For request bodies.
- @RequestHeader: For HTTP headers.
- @CookieValue: For cookies.
- @ModelAttribute: For form data and model attributes.
- @SessionAttributes: For session attributes.
- @RequestPart: For multipart request parts.
</details>


<details>
  <summary>What are the valid return types of a controller method?</summary>

- String
- ModelAndView, View
- @ModelAttribute
- void
- HttpEntity<B>, ResponseEntity<B>
- @ResponseBody
- HttpHeaders
- ErrorResponse
- ProblemDetail
- DeferredResult<V>, Callable<V>, CompletableFuture<V> and etc
- StreamingResponseBody
</details>
