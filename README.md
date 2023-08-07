# Pre-Initialization of Servlet in Java

This Java project demonstrates how to implement pre-initialization of a servlet. We will create a Dynamic Web Project and create a servlet named `PreInitServlet`.
This servlet will have an `init()` method, and we will observe how this method is called during `Lazy Initialization` or `Pre-Initialization`.

## Project Setup

1. Create a new dynamic web project in your Java IDE (e.g., Eclipse, IntelliJ, etc.).
2. Make sure you have Tomcat set up in your IDE. (Don't have Tomcat set up? [Check This](https://github.com/AryabhattSingh/Download-Configure-Tomcat-In-Eclipse#how-to-download-and-configure-apache-tomcat-in-eclipse))

## PreInitServlet

The `PreInitServlet` is a servlet that contains an `init()` method and a `doGet()` method. The purpose of this servlet is to demonstrate pre-initialization and lazy initialization behavior.

### init() Method

The `init()` method of the `PreInitServlet` is called when the servlet is initialized by the web container. It simply contains a print statement to indicate when this method is executed.

### doGet() Method

The `doGet()` method of the `PreInitServlet` contains a `PrintWriter` object which sends a character stream back to the web browser as a response.

## Lazy Initialization

By default, all servlets are lazy initialized. It means that unless and until there is a client request, the servlet will remain instantiated, but not initialized.

When we restart the Tomcat server and check the Tomcat console, we won't see any output from the `init()` method. This indicates that the servlet is only instantiated but 
not initialized at this point. The actual initialization, and thus the output from `init()`, will happen only when we access the servlet from the web browser.

## Pre-Initialization

Pre-Initialization means that the servlet will be initialized even before any client request comes in. The servlet will be initialized on application start-up.

The output from the `init()` method will be visible in the Tomcat console when we restart the server without actually launching the application. 

#### How to restart the server without running the application?
    At the bottom of the screen, there will be the Server view.
    Click on the green-colored ▶ button on the right-hand side of the screen.
    This will restart the Tomcat server.

To achieve the pre-initialization of a servlet, we can use either of the following -
 - the `loadOnStartup` attribute in the `@WebServlet` annotation or
 - `<load-on-startup>` element in the `<servlet>` element in the `web.xml` file.

### Using `@WebServlet` Annotation

In the `PreInitServlet` class, we can specify the `loadOnStartup` attribute in the `@WebServlet` annotation. This attribute takes a non-negative number as its value. 
The lower the number, the higher the priority of the servlet to be loaded on web container startup. If we provide a negative number, the servlet will be lazily initialized.

```java
@WebServlet(name = "PreIntialization", urlPatterns = { "/preInitServlet" }, loadOnStartup = 1)
public class PreInitServlet extends HttpServlet {
    // ...
}
```

### Using `web.xml`

Alternatively, we can achieve pre-initialization by configuring the `<load-on-startup>` element in the `web.xml` file. Set its value to a non-negative number to specify the 
priority of the servlet to be loaded during web container startup.

```xml
<servlet>
    <servlet-name>PreIntialization</servlet-name>
    <servlet-class>your.package.path.PreInitServlet</servlet-class>
    <load-on-startup>1</load-on-startup>
</servlet>

<servlet-mapping>
    <servlet-name>PreIntialization</servlet-name>
    <url-pattern>/preInitServlet</url-pattern>
</servlet-mapping>
```

## When to Use Pre-Initialization

Pre-initialization is useful when we want to perform some actions in the servlet even before any request comes from the web browser. This allows us to set up necessary 
resources or perform other tasks that should be ready when the servlet starts handling requests.

<br>
<br>

Feel free to explore this Java project and observe the behavior of pre-initialization and lazy initialization in the `PreInitServlet`. If you have any questions or 
suggestions, please don't hesitate to reach out.

Happy coding!
