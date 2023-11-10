# Learn To Build Java Spring Application

##  🔑 Key Concepts:
    
### 🛠️ Spring Boot:
Spring Boot is like a special tool that makes it much easier to create web applications using the Spring Framework. Think of it as a helper that takes care of many boring and repetitive tasks, so you can focus on writing the actual code for your application.

### 📁 Spring Initializr:
It's a web-based tool that helps you generate a Spring Boot project with the desired dependencies and configurations https://start.spring.io/.
![image](https://github.com/tauh33dkhan/LearnToBuildJavaSpringApplication/assets/43419559/d891ab4d-c9a8-412b-97a6-45c31768abb1)

### @ Annotations:
Annotations are used to simplify configuration and reduce the need for XML configuration files. Annotations are used to define beans, configure components, and specify request mappings, among other things. Here's an example

```java
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestControllerr
public class MyController {

    @GetMapping("/example")
    public String getExample() {
        return "This is a GET endpoint example!";
    }
}
```
In this example:

`@RestController`: This annotation is used to indicate that the class is a Spring MVC controller. It plays a role similar to the XML configuration <mvc:annotation-driven>.
`@GetMapping("/example")`: This annotation maps HTTP GET requests to the specified URI ("/example"). 

### 🛢👀🕹️ MVC (Model-View-Controller):
Modern application follows the MVC architectural pattern, which separates an application into three components: Model (data), View (presentation), and Controller (request handling).

### 🎮 Controller:
A controller is a Java class that handles incoming HTTP requests and returns an HTTP response. In the following example the @RestController annotation indicates that the class is a REST controller, and the @GetMapping annotation specifies the mapping of the method to a URL path.

```java
@RestController
public class logoutController {
    @GetMapping("/logout")
    public String logout(HttpSession session){
        session.invalidate();
        return "redirect:/login";
    }
}
```

### Entity Class:
An entity class is a Java class that corresponds to a database table. It is annotated with @Entity and defines fields that map to columns in a particular table. An entity class is used in Java Persistence API (JPA) to represent and interact with database tables, and it typically represents a specific type of data within your application. Let's create an example of a User entity class. This class will represent users in a application and will include fields such as id, username, email, and password.

```java
package com.learn.helloworld;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;

@Entity
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String username;
    private String email;
    private String password;

    // Getters
    public Long getId() {
        return id;
    }
    
    public String getUsername() {
        return username;
    }
    ...
    // Setters
    public void setId(Long id) {
        this.id = id;
    }

    public void setUsername(String username) {
        this.username = username;
    }
    ...
}
```

### JPARepository:

JpaRepository is an interface provided by Spring Data JPA, that simplifies database access in Spring applications by offering a set of standard CRUD (Create, Read, Update, Delete) operations for working with JPA (Java Persistence API) entities.

```java
import org.springframework.data.jpa.repository.JpaRepository;

public interface UserRepository extends JpaRepository<User, Long> {
    // You can add custom query methods here if needed
    User findByUsername(String username);
    // Additional query methods based on your requirements
    @Query("SELECT u FROM User u WHERE u.email = :email AND u.user = :password")
    User findByEmailAndPassword(@Param("email") String email, @Param("password") String password);
}
```

Here are some key features and benefits of using JpaRepository:

**Standard CRUD Operations:** JpaRepository provides methods like save, findAll, findById, delete, and more, which allow you to perform common database operations without writing SQL queries. These methods are type-safe and automatically generate SQL queries based on method names.

**Custom Query Support:** In addition to standard CRUD methods, you can define custom query methods in your repository interfaces, allowing you to perform more complex database operations. You can annotate these methods with @Query to define JPQL (Java Persistence Query Language) queries or native SQL queries if needed.

**Pagination and Sorting:** JpaRepository supports pagination and sorting of query results, making it easy to retrieve a subset of data or sort results based on specific criteria.

### </> pom.xml:

The pom.xml file is a configuration file which is used to manage project dependencies, build settings, and plugins. It defines what libraries the application needs, how to build the application, and various project details like its name and version. The file plays a central role in simplifying project management and ensuring consistent builds.

### 🏁 Starting Point:
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

**Step 1:** Set up the Project.

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

![image](https://github.com/tauh33dkhan/Learn-To-Build-Java-Spring-Application/assets/43419559/8637ef0d-3951-4c7f-b506-61e6f39a4ee2)


**Step 2:** Before starting to add code first check if you have created proper spring project with right dependency and java version by starting the spring application using following command.

```bash
$ mvn spring-boot:run
```

If the application is build successfully it will start a localhost server on port 8080.

**Step 3:** Create a Controller for our hello world application.

Go to /src/main/java/com/learn and create a new java file helloWorldConroller.java. VSCode will automatically create a class declaration.

```java
// helloWorldConroller.java
package com.learn.helloworld;

public class helloWorldController {
    
}
```

Now we need to add code to use this class as a controller and display message `hello world` when someone visit our website. to do this we will add @RestController annonation before our class defination and use @GetMapping annoation to handle request coming for specific path.

```java
// helloWorldController.java
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

**Step 4:** Start server and make request to `/helloWorld` endpoint to check our helloworld application is working.

```bash
$ mvn spring-boot:run
```

![image](https://github.com/tauh33dkhan/Learn-To-Build-Java-Spring-Application/assets/43419559/39265c78-bb7d-452f-8e37-dc4e61dfcefd)


<hr>

## Handling Request Parameter

To handle request parameters coming from the user we can use the `@RequestParam` annotation. This annotation allows you to extract values from the request's query parameters and use them in your controller method. Here's how you can modify your helloWorldController to handle request parameters:

```java
// helloWorldController.java
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
    // Added mapping for sayMyName GET endpoint which takes user input from the URL parameters
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

In the above code we are using `@RequestParam` annonation to handle parameter coming from user. here, `firstName` is the GET parameter coming from user and its default value is set to Guest then we assign its value to String variable fName, similarly we handle the lastName parameter coming from the user and assign it to string variable lName.

Let's test it

```bash
$ mvn spring-boot:run
$ curl "http://localhost:8080/sayMyName?firstName=test&lastName=test"
Hello, test test!
```

![image](https://github.com/tauh33dkhan/Learn-To-Build-Java-Spring-Application/assets/43419559/bc923b18-d70b-40ef-bea4-174ca6a9fc97)

We can also access request parameters by using the `@RequestParam Map<String, String>` params approach. This approach allows you to collect all request parameters into a Map. Here's an example:

```java
// helloWorldController.java
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
Create an HTML template (e.g., hello.html) in your `src/main/resources/templates directory`. This template will be used to render the response:

```html
// hello.html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Hello Page</title>
</head>
<body>
    <h1 th:text="'Hello, ' + ${username} + '!'"></h1>
</body>
</html>
```

Modify your controller to return the HTML template:

```java
// helloWorldController.java
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;

@Controller
public class HelloWorldController {
    @GetMapping("/helloWorld")
    public String sayHello(@RequestParam(name = "username", defaultValue = "Guest") String username, Model model) {
        model.addAttribute("username", username);
        return "hello"; // This corresponds to the "hello.html" template
    }
}
```
In this modified code:

- We've changed the `@RestController` annotation to `@Controller` to indicate that this class is responsible for returning views.
- We've added the Model parameter to the `sayHello` method to pass data to the view. We use `model.addAttribute` to pass the `username` variable to the template.

Now, when you access `/helloWorld?username=John`, the controller will use the `hello.html` template to display "Hello, John!" in an HTML page. If no "name" parameter is provided, it will default to "Hello, Guest!" in the HTML page. Thymeleaf's `th:text` attribute is used to populate the `<h1>` tag with the dynamic content.

![image](https://github.com/tauh33dkhan/Learn-To-Build-Java-Spring-Application/assets/43419559/705da491-a7c3-47e3-a6a2-eb07e329aa64)


### Secure code review:

Thymeleaf `th:text` expression autoescapes the user supplied input to protect against XSS attacks but if the application is using `th:utext` it will display the unescaped user supplied input, including any HTML or special characters.

<hr>

## User registration

Creating a registration functionality in a Spring web application typically involves several steps, including creating the registration form, processing user input, and storing user data. Here, I'll provide a simplified example to get started.

**STEP 1:** Create a controller `registerControler.java` in `src/main/java/com/learn/helloworld` path to handle request to GET `/register` endpoint.

```java
// registerController.java
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

**STEP 2:** Create `register.html` template in `src/main/resources/templates` path

```html
// register.html
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

**STEP 3:** Handle the registration POST request using the `@PostMapping` annotation. Store the username in the session for the demo, then redirect the user to the `/dashboard` endpoint using return `redirect:/dashboard";`. Handle the dashboard request by first retrieving the username value from the session and displaying it using the `dashboard.html` template.

```java
// registerController.java
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

<hr>

## Store user registration data in database

### Step 1: Add Dependencies to `pom.xml`

In your pom.xml, include dependencies for Spring Boot Data JPA and a database driver. For this example, we'll use mariadb as the embedded database:

```xml
<dependencies>
    <!-- Spring Boot Data JPA -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
    <dependency>
        <groupId>org.mariadb.jdbc</groupId>
        <artifactId>mariadb-java-client</artifactId>
        <version>2.7.4</version> <!-- Use the latest version available -->
    </dependency>
</dependencies>
```

### STEP 2: Configure Database Properties

In your `application.properties` file, configure your database properties. Below is an example of H2 database configuration. For a production application, you'd replace these settings with your actual database details:

```bash
# DataSource settings
spring.datasource.url=jdbc:mariadb://localhost:3306/helloworlddb
spring.datasource.username=user
spring.datasource.password=password
spring.datasource.driver-class-name=org.mariadb.jdbc.Driver
spring.jpa.hibernate.ddl-auto=update
```

### STEP 3:  Create an Entity Class

Create an entity class `User` in `src/main/java/com/learn/helloworld/` path representing the user registration data. Annotate it with @Entity, and define fields for user data:

```java
package com.learn.helloworld;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;

@Entity
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String username;
    private String email;
    private String password;

    //Getters and setters
    public Long getId() {
        return id;
    }
    
    public String getUsername() {
        return username;
    }

    public String getEmail() {
        return email;
    }

    public String getPassword() {
        return password;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public void setPassword(String password) {
        this.password = password;
    }

}

```

### STEP 4: Create a Repository Interface

Create a repository interface by extending JpaRepository. This interface provides CRUD (Create, Read, Update, Delete) operations for your `User` entity:

```java
// src/main/java/com/learn/helloworld/UserRepository.java
package com.learn.helloworld;

import javax.persistence.LockModeType;

import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.data.jpa.repository.Lock;

public interface UserRepository extends JpaRepository<User, Long>{
    User findByUsername(String username); // interface for User entitiy
    // Additional custom queries can be added here if needed
}
```

### STEP 5: Modify the Registration Controller

Modify your registration controller to use the repository to save user data to the database:

```java
// registerController.java
package com.learn.helloworld;

import javax.servlet.http.HttpSession;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestParam;

@Controller
public class registerController {
    @Autowired
    private UserRepository userRepository;    
    
    @GetMapping("/register")
    public String register() {
        return "register";
    }
    // @Transactional
    @PostMapping("/register")
    public String registerUser(@RequestParam String username, @RequestParam String email, @RequestParam String password, HttpSession session, Model model) {
        User user = new User();
        User user1 = userRepository.findByUsername(username); // Get user details from database to avoid duplicate registration
        if (user1 != null){    // Check if the user with same username already registered
            return "redirect:/register?msg=User Already Registered";
        } 
        user.setUsername(username);    // Set user supplied details to user
        user.setEmail(email);
        user.setPassword(password);
        try {
            userRepository.save(user);      // Save user details
        } catch (Error e){    // print exception in console
            System.out.println(e);    
            return "redirect:/register?msg=An error occured while registering user";  
        }
        session.setAttribute("username", username);    // set username in session
        return "redirect:/dashboard";
    }
}
```

### STEP 6: Update `dashboardController` and `dashboard.html` and also add logout controller to invalidate user session.

```java
// dashboardController.java
package com.learn.helloworld;

import javax.servlet.http.HttpSession;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;

@Controller
public class dashboardController {
    @Autowired
    private UserRepository userRepository;
    
    @GetMapping("/dashboard")
    public String dashboard(HttpSession session, Model model) {
        String username = (String) session.getAttribute("username");
        // Check if a username is stored in the session
        if (username == null) {
            return "redirect:/register";
        }
        // Get user details from database
        User user = userRepository.findByUsername(username);       
        if (user == null) {
            return "redirect:/register";
        }
        System.out.println("ADAD"+ user.getUsername());
        model.addAttribute("user", user);
        System.out.println(user);
        return "dashboard";
    }
}
```

```java
// dashboard.html
<html>
    <center>
        <h1 th:text="'Hello, ' + ${user.getUsername()} + '!'"></h1>
        <form action="/logout" method="GET">
            <input type="submit" value="Logout">
        </form>
    </center>
</html>
```

```java
// logoutController.java
package com.learn.helloworld;

import javax.servlet.http.HttpSession;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;

@Controller
public class logoutController {
    @GetMapping("/logout")
    public String logout(HttpSession session){
        session.invalidate();
        return "redirect:/login";
    }
}
```
### STEP 7: Build the application and test the registration and logout functionality.

![image](https://github.com/tauh33dkhan/Learn-To-Build-Java-Spring-Application/assets/43419559/aae0cd88-3d09-420b-81a4-3091a037f324)


![image](https://github.com/tauh33dkhan/Learn-To-Build-Java-Spring-Application/assets/43419559/d81104c5-3546-4696-807b-bd00372f5c76)


What's NEXT? I will start implementing vulnerabilities and document vulnerable code..
