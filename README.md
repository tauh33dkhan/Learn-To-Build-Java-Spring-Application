# helloWorldSpringApplication

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


### Creating a Hello World Spring Application

Step 1: Set up the Project.

Use Spring Initializer to set up the project with Maven. Visit Spring Initializer(https://start.spring.io/) and create a new project with the following options:
```
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
```
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

### Handling Request Parameter

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
Using @RequestParam to handle parameter coming from user here `firstName` is the GET parameter coming from user and its default value is set to Guest then we assign its value to String variable fName similarly we handle the lastName coming from user and assign it to string variable lName


