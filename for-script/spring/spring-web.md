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
