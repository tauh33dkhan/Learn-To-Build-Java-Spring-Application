# Learn To Build Java Spring Application

## Key Concepts:

### Spring Boot: 
Spring Boot is like a special tool that makes it much easier to create web applications using the Spring Framework. Think of it as a helper that takes care of many boring and repetitive tasks, so you can focus on writing the actual code for your application.

### Spring Initializr:
It's a web-based tool that helps you generate a Spring Boot project with the desired dependencies and configurations https://start.spring.io/.

### Annotations: 
annotations are used to simplify configuration and reduce the need for XML configuration files. Annotations are used to define beans, configure components, and specify request mappings, among other things.

### MVC (Model-View-Controller): 
Modern application follows the MVC architectural pattern, which separates an application into three components: Model (data), View (presentation), and Controller (request handling).

### Controller: 
A controller is a Java class that handles incoming HTTP requests and returns an HTTP response. In the following example the @RestController annotation indicates that the class is a REST controller, and the @GetMapping annotation specifies the mapping of the method to a URL path.
```java
// helloworldController.java
package com.example.demo;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class controller {
    @GetMapping("/") 
    String return1(){ 
        return "Hello World"; 
    } 
}
```

### pom.xml:
The pom.xml file is a configuration file which is used to manage project dependencies, build settings, and plugins. It defines what libraries the application needs, how to build the application, and various project details like its name and version. The file plays a central role in simplifying project management and ensuring consistent builds.

### Starting Point:

Here's how Spring Boot determines the entry point class:
- Spring Boot looks for a class with a public static void main(String[] args) method. This method is the starting point for any Java application. It's where the application's execution begins.
- Spring Boot checks the presence of the @SpringBootApplication annotation on the class that contains the main method.
- Once Spring Boot finds the class with the @SpringBootApplication annotation and a main method, it runs the application by invoking the main method in that class.

Here's an example of a typical Spring Boot entry point class:
```java
package com.example.demo;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class MySpringBootApplication {
    public static void main(String[] args) {
        SpringApplication.run(MySpringBootApplication.class, args);
    }
}
```

In this example, the class MySpringBootApplication is marked with the @SpringBootApplication annotation, and it contains the main method. Spring Boot identifies it as the entry point for the application, and the main method initiates the Spring Boot application.

<hr>

## Creating a Hello World Spring Application

Step 1: Set up the Project.

Use Spring Initializer to set up the project with Maven. Visit Spring Initializer(https://start.spring.io/) and create a new project with the following options:
```bash
Project: Maven
Language: Java
Spring Boot: 2.7.17
Packaging: JAR
Java: 8
Dependencies: Spring Web
Group: com.learn
Artifact: helloworld
```
Click on generate it will create a Spring Boot project with the desired dependencies and configurations.
Unzip the downloaded project and open it in VSCode. Navigate through the files to understand the default files, why they are there and the skelaton code proivded.

Step 2: Before starting to add code first check if you have created proper spring project with right dependency and java version by starting the spring application using following command
```bash
$ mvn spring-boot:run
```
If the application is build successfully it will start a localhost server on port 8080.

Step 2: Create a Controller for our hello world application.

Go to /src/main/java/com/learn and create a new java file helloWorldConroller.java. VSCode will automatically create a class declaration.
```java
// helloWorldConroller.java
package com.learn.helloworld;

public class helloWorldController {
    
}
```

Now we need to add code to use this class as a controller and display message `hello world` when someone visit our website. to do this we will add @RestController annonation before our class defination and use @GetMapping annoation to handle request coming for specific path.
```java
package com.learn.helloworld;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;


@RestController
public class helloWorldController {
    @GetMapping("/helloWorld")
    public String sayHello() {
        return "hello world";
    }
}
```

Step 3: Start server
```bash
$ mvn spring-boot:run
$ curl localhost:8080/helloWorld
hello test  
```

<hr>

## Handling Request Parameter

To handle request parameters coming from the user we can use the @RequestParam annotation. This annotation allows you to extract values from the request's query parameters and use them in your controller method. Here's how you can modify your helloWorldController to handle request parameters:

```java
package com.learn.helloworld;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;


@RestController
public class helloWorldController {
    @GetMapping("/helloWorld")
    public String sayHello() {
        return "hello test";
    }
    // Added mapping for sayMyName GET endpoint which takes user input from name parameter
    @GetMapping("/sayMyName")
    public String sayMyName(
        @RequestParam(name = "firstName", defaultValue = "Guest") String fName,
        @RequestParam(name = "lastName", defaultValue = "User") String lName){
        return "Hello, " + fName + " "+ lName +"!";
    }
}
```
Let's break down the code:

```java
@RequestParam(name = "firstName", defaultValue = "Guest") String fName
```

Using @RequestParam annonation to handle parameter coming from user. here, `firstName` is the GET parameter coming from user and its default value is set to Guest then we assign its value to String variable fName, similarly we handle the lastName parameter coming from user and assign it to string variable lName.

```bash
$ mvn spring-boot:run
$ curl "http://localhost:8080/sayMyName?firstName=test&lastName=test"
Hello, test test!
```

We can also access request parameters by using the `@RequestParam Map<String, String>` params approach. This approach allows you to collect all request parameters into a Map. Here's an example:
```java
package com.learn.helloworld;

import java.util.Map;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;


@RestController
public class helloWorldController {
    // Added mapping for sayMyName GET endpoint which takes user input from name parameter
    @GetMapping("/sayMyName")
    public String sayMyName(@RequestParam Map<String, String> params){
        String firstName = params.get("firstName");
        String lastName = params.get("lastName");
        return "Hello, " + firstName + " "+ lastName +"!";
    }
}
```

### Using view to display HTML content

If you want to display the response in an HTML page instead of returning a plain string, you can modify your Spring MVC controller to return a view. You will need to create a Thymeleaf HTML template to render the content. Here's how you can do it:

First, make sure you have Thymeleaf as a dependency in your project. You can add it to your pom.xml file:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-thymeleaf</artifactId>
</dependency>
```
Create an HTML template (e.g., hello.html) in your src/main/resources/templates directory. This template will be used to render the response:

```html

<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Hello Page</title>
</head>
<body>
    <h1 th:text="'Hello, ' + ${userName} + '!'"></h1>
</body>
</html>
```

Modify your controller to return the HTML template:

```java

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;

@Controller
public class HelloWorldController {
    @GetMapping("/helloWorld")
    public String sayHello(@RequestParam(name = "name", defaultValue = "Guest") String userName, Model model) {
        model.addAttribute("userName", userName);
        return "hello"; // This corresponds to the "hello.html" template
    }
}
```
In this modified code:

- We've changed the `@RestController` annotation to `@Controller` to indicate that this class is responsible for returning views.
- We've added the Model parameter to the sayHello method to pass data to the view. We use model.addAttribute to pass the userName variable to the template.

Now, when you access `/helloWorld?name=John`, the controller will use the hello.html template to display "Hello, John!" in an HTML page. If no "name" parameter is provided, it will default to "Hello, Guest!" in the HTML page. Thymeleaf's `th:text` attribute is used to populate the `<h1>` tag with the dynamic content.

### Secure code review:

Thymeleaf `th:text` expression autoescapes the user supplied to protect against XSS attacks but if the application is using `th:utext` it will display the unescaped user supplied input, including any HTML or special characters.

<hr>

## User registration

Creating a registration functionality in a Spring web application typically involves several steps, including creating the registration form, processing user input, and storing user data. Here, I'll provide a simplified example to get started.

STEP 1: Create a controller `registerControler.java` to handle request to GET `/register` endpoint.

```java
// registerController
package com.learn.helloworld;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;


@Controller
public class registerController {
    @GetMapping("/register")
    public String register() {
        return "register";
    }
}

```

STEP 2: Create `register.html` template
```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Registration</title>
</head>
<body>
    <h2>Registration</h2>
    <form action="/register" method="post">
        <label for="username">Username:</label>
        <input type="text" id="username" name="username" required /><br>
        
        <label for="password">Password:</label>
        <input type="password" id="password" name="password" required /><br>
        
        <button type="submit">Register</button>
    </form>
</body>
</html>
```

STEP 3: Handle registration post request using @PostMapping annonation and store the username in session for demo then redirect the user to `/dashboard` using `return "redirect:/dashboard";` then handle dashboard request, first get the username value from session and display it using `dashboard.html`.

```java
package com.learn.helloworld;

import java.util.HashMap;
import java.util.Map;

import javax.servlet.http.HttpSession;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestParam;

@Controller
public class registerController {

    @GetMapping("/register")
    public String register() {
        return "register";
    }

    @PostMapping("/register")
    public String registerUser(@RequestParam String username, @RequestParam String password, HttpSession session) {
        session.setAttribute("username", username);  // storing username in ssession
        return "redirect:/dashboard";    // redirecting user to dashboard after registration
    }

    @GetMapping("/dashboard")
    public String dashboard(HttpSession session, Model model) {
        model.addAttribute("username", session.getAttribute("username"));    // getting user detail from session
        return "dashboard"; 
    }
}

```

```java
//dashboard.html
<html>
    <center>
        <h1 th:text="'Hello, ' + ${username} + '!'"></h1>
    </center>
</html>
```
