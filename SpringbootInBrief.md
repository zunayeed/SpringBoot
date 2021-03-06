						# Springboot
## Question: what is @SpringBootApplication annotation ? 
Many Spring Boot developers like their apps to use 
*  auto-configuration, 
*  component scan and
*  be able to define extra configuration on their "application class".
         
 ## A single @SpringBootApplication annotation can be used to enable those three features:
1. @EnableAutoConfiguration: enable Spring Boot’s auto-configuration mechanism
2. @ComponentScan: enable @Component scan on the package where the application is located 
3. @Configuration: allow to register extra beans in the context or import additional configuration classes

So, @SpringBootApplication annotation is equivalent to using @EnableAutoConfiguration, @ComponentScan, and @Configuration  with their default attributes, as shown in the following example:

```java
package com.example.myapplication;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
@SpringBootApplication // same as @Configuration @EnableAutoConfiguration @ComponentScan
public class Application {

public static void main(String[] args) {
SpringApplication.run(Application.class, args);
```

- SpringApplication.run launches a Springboot application
    
    
### Step 2: 
`@RequestMapping(value = "/login", method = RequestMethod.GET)`
 ` http://localhost:8080/login`
Question:  Why `@ResponseBody` annotation is usedf for?
Answer:  The `@ResponseBody` annotation tells a controller that the object returned is automatically serialized into JSON and passed back into the HttpResponse object.
`@ResponseBody` is a Spring **annotation** which binds a method return value to the web **response body**. It is not interpreted as a view name. It uses HTTP Message converters to convert the return value to HTTP ****response body**, based on the content-type in the request HTTP header

![MVC-Flow](https://docs.spring.io/spring-framework/docs/2.0.8/reference/images/mvc.png)

Important of RequestMapping method
    //How do web applications work? Request and Response
    //Browser sends Http Request to Web Server
    //Code in Web Server => Input:HttpRequest, Output: HttpResponse
    //Web Server responds with Http Response

----------------------------------------------------------------------------------------------------------------------
spring is popular because 
	    1) Enables writing testable codes
	          - enables  writing good unit test so easily
	   2) No plumbing code: trycatch block, lots of line of code, but in spring it is almost nothin
           3) Architectural flexibility: strong modular concept 
           4) Follows current trend: spring boot helps develpo microservices very easily

- Maven is used to manage the dependency of Java projects 
- Springboot is one of the most popular spring framework to develop micro services.


# Group Id: package name 
# Artifact Id: Project name 
- SpringApplication.run launches a Springboot Application
- `spring-boot-starter-parent` has all default configuration of all important maven dependencies
- Spring Boot Starter Web provides: 1) all dependies to run web applications: core, mvc, validation,login 
Dev tools helps developer in saving time

## MVC: 
1.  When dispatcher servlet receives  a request  coming as  `/login`, it sends the request to  LoginController's loginMessage method because `/login` is mapped to it. 

2. dispatcher servlet gets this login, and due to @ResponseBody, dispatcher servlet will directly return this content to the browser.

      dispatcherServlet does not know the path of login.jsp. It search for a view named "login".

     HOW do we let dispatcherServlet know that this view is in this specific path:
      login.jsp path:  /src/main/webapp/WEB-INF/jsp/login.jsp . 
      "login"  =>  /src/main/webapp/WEB-INF/jsp/login.jsp 

Now the view resolver concept comes into picture. Whenever controller return login, it need to map in to specific login.jsp file.  
	
 In spring, we use application.properties, by using a view resolver
		Second Snippet(Location of application.properties file):     
		                     `   -/src/main/resources/application.properties`
Code addressed in  application.properties file: 
```properties
		spring.mvc.view.prefix: /WEB-INF/jsp/
		spring.mvc.view.suffix: .jsp
		logging.level.: DEBUG
```
### Question: What is **viewResolver**? 
View Resolver function: view resolver maps logical name to a physical jsp 
- provided by all MVC Frameworks, 
- Render models to browser, 
- without being tied to a specific view technology. 
- Spring MVC Framework provides the ViewResolver interface, that maps view names to actual views.

It also provides the View interface, which addresses the request of a view to the view technology. So, when a ModelAndView instance is returned by a Controller, the view resolver will resolve the view according to the view.

* Enabling jsp support in embedded tomcat server: **add  tomcat-embed-jasper dependency** in the pom.xml file. 
```
        <dependency>
            <groupId>org.apache.tomcat.embed</groupId>
            <artifactId>tomcat-embed-jasper</artifactId>
            <scope>provided</scope>
        </dependency>
```
Still no update, because springboot developer tools can only handle changes within the application. When we change pom.xml, we are changing the dependency, or jar files. In this kind of situation, we **need to restart** the whole application.
```
   	server.port=8082
	spring.mvc.view.prefix=/jsp/
	spring.mvc.view.suffix=  .jsp
	logging.level.org.springframework.web: DEBUG
```

> when we pass variable to chrome address bar in login, how does it go to controller ? at controller, we use @RequestParam annotation, so we want to bind the request parameter, in import it is web.bind.annotation.RequestParam
   get request > controller > view 
then it shows the result in the console, not in jsp view. in order to make it available to view, in spring mvc we use model .

 **Model** is used to pass data from controller to view (JSP). So, we need to put the data in the model so that we can pass it to the view. 

Controller controls the entire flow, once it has data, it puts it to the model, and redirects it to the view. The view uses the model to render the data. 

So, once the name through the @RequestParam annotation comes into the controller, we need to put it in model. In order to put it in model, we  need to have ModelMap object passed in to the method parameter. As a argument of  model.put()passed as input parameter, we mention the attribute and value. So, whatever you mention in the put, it will be available in the jsp. So, in order to access the value of variable in JSP, we use expression language ${<variable_name>}

Any request that comes to web application, it comes to the front controller. 

 ![center](http://docs.spring.io/spring-framework/docs/2.0.8/reference/images/mvc.png)

Question:  Why Get Method is not secure? 
Answer: Get method is not secure, we can see data in the url. in internet data travels from router to router, so data can be seen easily. So the ideal solution is using post. 


                                                  Useful Annotation used in bean: 
1. @Component:  to create bean autometically for a particular class and if you use @component annotation for a class, you are requesting spring to manage it
2. @Service is used for business logic
3. @Repository for storing data to database, JPA
4. @Controller - if bean handle request from browser
5. @Autowired - to declare dependent componet of bean, 
6. @ComponentScan @SpringbootApplication has componenscan builtin - spring search component within the package

**Spring framework is all about finding your component and autowiring components.** 

**If you want to store something across multiple pages, then session comes into picture.**

-------------------------------------------------------------------------------------------------------------

when user types /login. we want to send them back "Hello world"

the way we do : 
1. create a login controller class
2. create a method to map request(/login) 
3. add annotation to class(@Controller) and method (@RequestMapping  @ResponseBody )
               
```java               
package com.zunayeed.springboot.web.controller;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
public class LoginController {
	
	int a = 3;
	int b =5 ;
	@RequestMapping("/login")
	@ResponseBody 
	public String loginMessage() {
		return "Hello Zuayeed, Welcome to springboot applications: " + (a+b) ; 		
	}
}
```


>>>>      To see spring level debug: 
                                    ` src/main/resources/application.properties`
                                    `  logging.level.org.springframework.web: DEBUG`

 1) Set up login.jsp file : 
First Snippet - /src/main/webapp/WEB-INF/jsp/login.jsp
```html
<html>
<head>
<title>Yahoo!!</title>
</head>
<body>
My First JSP!!!
</body>
</html>
```
2) add dependency to application.properties file 
Second Snippet - /src/main/resources/application.properties

spring.mvc.view.prefix: /WEB-INF/jsp/
spring.mvc.view.suffix: .jsp
logging.level.: DEBUG

3) to enable jsp support, add the dependency
Third Snippet : To enable jsp support in embedded tomcat server!
```
<dependency>
<groupId>org.apache.tomcat.embed</groupId>
<artifactId>tomcat-embed-jasper</artifactId>
<scope>provided</scope>
</dependency>
```
        
        
        
        
                              5 What You Will Learn during this Step:
You first GET Parameter.
Problem with using GET
Snippets
ModelMap model
model.put("name", name);
My First JSP!!! My name is ${name}

          >>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>
     
## Question:  What is @RequestParam in spring?
Spring MVC RequestParam Annotation:  In Spring MVC, the @RequestParam annotation is used to read the form data and bind it automatically to the parameter present in the provided method. So, it ignores the requirement of HttpServletRequest object to read the provided data.
       
 **Model is used to pass data from controller to view(JSP).**  
 we need to put the data in the model so that we can pass it to the view. So the controller controls the entire flow, once it has some data, it puts it to the model, and model redirects it(data) to the view. The view uses the model to render the data. 

So, once the data(String name) -through the @RequestParam annotation- comes into the controller, we need to put it in model. In order to put it in model, we  need to have ModelMap object(ModelMap model) passed in to the @RequestMapping-annotated-method parameter as an input argument.


In `model.put("name", value); `,  we mention the attribute and value as name of parameter as name. 

So whatever you mention in the model.put("name", value), it will be available in the jsp. So, in order to access the value of variable in JSP(login.jsp) , we use expression language ${<variable_name>} ${name}

In brief 
 a ) the steps in controller
 ```java
package com.zunayeed.springboot.web.controller;

import org.springframework.stereotype.Controller;
import org.springframework.ui.ModelMap;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
public class LoginController {
	
	int a = 3;
	int b =5 ;
	@RequestMapping("/login")	
	public String loginMessage(@RequestParam String name, ModelMap model) {
		model.put("name", name);
		System.out.println("name is" + name);
		return "login" ; 		
	}
}
```

b) file is in jsp: 

```                          src/main/webapp/WEB-INF/jsp/login.jsp
<html>
<head>
<title>Welcome to Login Portal</title>
</head>
<body>
Welcome to Simple login portal 
Here you will get value from model ${name}
</body>
</html>

```



                                           Spring MVC Request Flow
1. DispatcherServlet receives HTTP Request.
2. DispatcherServlet identifies the right Controller based on the URL mapping
3. Controller executes Business Logic.and puts data into model 
4. Controller returns **a) Model b) View Name** Back to DispatcherServlet.
5. DispatcherServlet identifies the correct view (ViewResolver).
6. Viewresolver maps logical name to physical jsp using the help from application.properties file.
        spring.mvc.view.prefix: /WEB-INF/jsp/
        spring.mvc.view.suffix: .jsp
7. DispatcherServlet makes the model available to view and executes it.
8. DispatcherServlet returns HTTP Response Back.
 ![center](http://docs.spring.io/spring-framework/docs/2.0.8/reference/images/mvc.png)
 
##Question: what is @RequestMapping Annotation ? What is its use ? 
- Spring @RequestMapping  annotation maps HTTP requests to handler methods of MVC and REST controllers.
- In Spring MVC applications, the RequestDispatcher (Front Controller Below) servlet is responsible for routing incoming HTTP requests to handler methods of controllers.When configuring Spring MVC, you need to specify the mappings between the requests and handler methods.

To configure the mapping of web requests, you use the @RequestMapping annotation.The @RequestMapping annotation can be applied to class-level and/or method-level in a controller.The class-level annotation maps a specific request path or pattern onto a controller. You can then apply additional method-level annotations to make mappings more specific to handler methods.


                                 Using @RequestMapping with HTTP Method
				 
The Spring MVC @RequestMapping annotation is capable of handling HTTP request methods, such as GET, PUT, POST, DELETE, and PATCH.
By default all requests are assumed to be of HTTP GET type.
In order to define a request mapping with a specific HTTP method, you need to declare the HTTP method in @RequestMapping using the method element as follows.
```java
@RestController
@RequestMapping("/home")
public class IndexController {
  @RequestMapping(method = RequestMethod.GET)
  String get(){
    return "Hello from get";                  
  }
  @RequestMapping(method = RequestMethod.DELETE)
  String delete(){
    return "Hello from delete";
  }
  @RequestMapping(method = RequestMethod.POST)
  String post(){
    return "Hello from post";
  }
  @RequestMapping(method = RequestMethod.PUT)
  String put(){
    return "Hello from put";
  }
  @RequestMapping(method = RequestMethod.PATCH)
  String patch(){
    return "Hello from patch";
  }
}
```
In the code snippet above, the method element of the @RequestMapping annotations indicates the HTTP method type of the HTTP request.
All the handler methods will handle requests coming to the same URL ( /home), but will depend on the HTTP method being used.
For example, a POST request to /home will be handled by the post() method. While a DELETE request to /home will be handled by the delete() method.

## @RequestMapping Shortcuts
				     
**Spring 4.3** introduced method-level variants, also known as composed annotations of **@RequestMapping**. The composed annotations better express the semantics of the annotated methods. They act as wrapper to @RequestMapping and have become the standard ways of defining the endpoints.

For example, **@GetMapping is a composed annotation that acts as a shortcut for @RequestMapping(method = RequestMethod.GET).**
The method level variants are:

- @GetMapping
- @PostMapping
- @PutMapping
- @DeleteMapping
- @PatchMapping


          >>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>
	                        Code for @RequestMapping  
	  
	  @Controller
public class LoginController {
	
	@RequestMapping(value="/login", method = RequestMethod.GET)
	public String showLoginPage(ModelMap model){
		return "login";
	}
	
	@RequestMapping(value="/login", method = RequestMethod.POST)
	public String showWelcomePage(ModelMap model, @RequestParam String name){
		model.put("name", name);
		return "welcome";
	}

}


					Step8
	             Add validation for userid and password
                           Hard coded validation!!
			   
 a) LoginController Class:  
```
@Controller
public class LoginController {
	
	@Autowired
	LoginService service;
		@RequestMapping(value="/login", method = RequestMethod.GET)
		public String showLoginPage(ModelMap model){
			return "login";
		}		
		@RequestMapping(value="/login", method = RequestMethod.POST)
		public String showWelcomePage(ModelMap model, @RequestParam String name, @RequestParam String password){			
			boolean isValidUser = service.validateUser(name, password);
			if (isValidUser) {
	            model.put("name", name);
	            model.put("password",password);
	            return "welcome";
	        } else {
	            model.put("errorMessage", 
		    "Invalid Credentials, Please enter correct User Name and password");
	            return "login";
	        }
		}
	}
```
b)Login validation in separate class: 
```java
@Component
public class LoginService {
	 public boolean validateUser(String user, String password) {
	        return user.equalsIgnoreCase("zunayeed") && password.equals("dummy");
	    }
}
```
c) login.jsp: 

```
<html>
<head>
<title>Welcome to Login Portal</title>
</head>
<body>
<font color="red">${errorMessage}</font>
<form method="post">
  Name : <input type="text" name = "name" /> 
  		 <input type="password" name = "password" />
  		<input type = "submit"/> 
```

d) Welcome.jsp: 
```
</form>
</body>
</html>
<html>
<head>
<title>Welcome Portal Application </title>
</head>
<body>
Welcome ${name}!! and you password is ${password}
</body>
</html>
```
			   			Step 
  Annotation used in bean: 
1. @Component:  to create bean autometically for a particular class and if you use @component annotation for a class, you are requesting spring to manage it. We can use @Component across the application to mark the beans as Spring's managed components. Spring only pick up and registers beans with @Component  and doesn't look for @Service and @Repository in general.

They are registered in ApplicationContext because they themselves are annotated with @Component:
@Component
public @interface Service {}
@Component
public @interface Repository {}

@Service and @Repository are special cases of @Component. They are technically the same but we use them for the different purposes.

2. @Service is used for business logic
3. @Repository for storing data to database, JPA
  @Repository’s job is to catch persistence specific exceptions and rethrow them as one of Spring’s unified unchecked exception.
4. @Controller - if bean handle request from browser
5. @Autowired - to declare dependent componet of bean, 
	     - without autowired, we get null pointer exception.
6. @ComponentScan:   @SpringbootApplication has componenscan builtin 
	            - spring search component within the package
		    - if you create component outside of package, it will not be autowired. 

                                      Spring Component
				      
In layman terms, a Component is responsible for some operations. Spring framework provides three other specific annotations to be used when marking a class as Component.

1. @Service: Denotes that the class provides some services. Our utility classes can be marked as Service classes.

1. @Repository: This annotation indicates that the class deals with CRUD operations, usually it’s used with DAO implementations that deal with database tables. 
           - used in terms of data store

1. @Controller: Mostly used with web applications or REST web services to specify that the class is a front controller and responsible to handle user request and return appropriate response.
          -if you are having request from browser, then @Controller
	  
Indicates that an annotated class is a "Controller" (e.g. a web controller). 

This(@Controller) annotation serves as a specialization of @Component,allowing for implementation classes to be autodetected through classpath scanning.It is typically used in combination with annotated handler methods based on the org.springframework.web.bind.annotation.RequestMapping annotation.



Note that all these four annotations are in package org.springframework.stereotype and part of spring-context jar.

Most of the time our component classes will fall under one of its three specialized annotations, so you may not use @Component annotation a lot
Spring framework is all about finding your component and autowiring components. If you want to store something across multiple pages, then session comes into picture.

  ## MVC  Architecture
 *  MVC Model 1 : Browser > JSP > Model
 Here the request is handled by JSP. JSP forward the request to another JSP, then it goes to model
 * Model 2: Request(Browser)> Servlet > Model > View . 
    - In Model 2, request redirects to servlets which are on the server 
 * Model 2 with Frontcontroller (evoluation):  
 - Browser > FrontController> Controller1>Model>Controller1>View1>FrontController>Browser
      - FrontController handles databinding, Handler Mapping, View Resolver and a lot of other    functionality
     - Here from the browser, request goes directly to a frontcontroller(DispatcherServlet in Spring MVC)
     - DispatcherServlet redirects the requests to different controller. For example /login to LoginController class. 
     - Based on URL, frontController decides with controller to go to. Once controller returns the databack, it decides which view to render, then it would send the response back to browser. So all data will be going through the front controller.    
     - view lecnology: Velocityu, JSF, FreeMarker, JSP/EL/JSTL
     - WebServices/ AngularJS
    -  Strusts/SpringMVC/MVC
     
    
   ##  Session is the way to store values across multiple request. 
   * **@SessionAttributes** annotation is used to store the model attribute in the session. 
     - used at controller class level.
          
   - Spring’s @SessionAttributes is used on a controller to designate which model attributes should be stored in the session. 
   - Htttp is a stateless protocol, so if you want to save any values, it need to be stored in server side in the session or some conversational storage.  
   
   - Spring documentation states that the @SessionAttributes annotation “list the names of model attributes which should be transparently stored in the session or some conversational storage.”
   
   - Why use Model? "adding elements directly to the HttpServletRequest (as request attributes) would seem to serve the same purpose. The reason to do this is obvious when taking a look at one of the requirements we have set for the MVC framework: It should be as view-agnostic as possible, which means we’d like to be able to incorporate view technologies not bound to the HttpServletRequest as well." - Rod Johnson et. al’s book Professional Java Development with the Spring Framework
  
       ----------------------------------------------------------------------------------
      
      when user types /login. we want to send them back "Hello world"

the way we do : 
  1) create a LoginController class
  2) create a method to map request(/login) 
  3) add annotation to class(@Controller) and method (@RequestMapping  @ResponseBody )
  4) Create a link list-todos in the welcome jsp page 
  5)Create a TodoController class with @Controller annotation. It needs TodoService 
  	* create a TodoService with @Autowired annotation: @Autowired TodoService Service
	     - import TodoService
	 * to configure the mapping of /list-todos web reruest, map it to a method with 
	    @RequestMapping(value="/list-todos, method = RequestMethod.GET) 
	 * using model.put(), retrieve  service.retrieveTodos()
	     model.put("todos", service.retrieveTodos("zunayeed"));
	 * create list-todos.jsp  with  ${todos}
	  
  6) Add `@SessionAttributes("name")` annotation in LoginController class and TodoController class, and it will make the name available to all subsequest classes(a way of storing values across multiple classes - Session) . 
       * Add this line inside  showTodos() of TodoController class
                 ` String name =  (String)model.get("name");`
		  `model.put("todos", service.retrieveTodos(name)); `
  
  ----------------------------------------------------------------------------------
  
  
  ![image](https://raw.githubusercontent.com/iPraBhu/ADevGuide/master/Resources/Spring%20Annotations%20Cheat%20Sheet%20ADevGuide.jpg)
 
 * step 13: 
 A better option is using the prefix redirect: – the redirect view name is injected into the controller like any other logical view name. The controller is not even aware that redirection is happening.
 
 ```
 @RequestMapping(value="/add-todo", method = RequestMethod.POST)
	public String addTodo(ModelMap model, @RequestParam String desc){
		service.addTodo((String) model.get("name"), desc, new Date(), false);
		return "redirect:/list-todos";
	}
```
 # step 14
 ## What we will do:
- Display Todos in a table using JSTL Tags
- <%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%>
- Add Dependency for jstl

## Snippet
```       
       <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>jstl</artifactId>
        </dependency>
```
		
# Step 15	
## webjars
WebJars are client side dependencies packaged into JAR archive files. They work with most JVM containers and web frameworks.
This question has a very simple answer – because it's easy.

Manually adding and managing client side dependencies often results in difficult to maintain codebases.

Also, most Java developers prefer to use Maven and Gradle as build and dependency management tools.

The main problem WebJars solves is making client side dependencies available on Maven Central and usable in any standard Maven project.

Here are a few interesting advantages of WebJars:

1. We can explicitly and easily manage the client-side dependencies in JVM-based web applications
2. We can use them with any commonly used build tool, eg: Maven, Gradle, etc
3. WebJars behave like any other Maven dependency – which means that we get transitive dependencies as well

## What we will do:
- Add bootstrap to give basic formatting to the page : We use bootstrap classes container,table and table-striped.
- We will use webjars
 - Already auto configured by Spring Boot : o.s.w.s.handler.SimpleUrlHandlerMapping  : Mapped URL path [/webjars/**] onto handler of type [class org.springframework.web.servlet.resource.ResourceHttpRequestHandler]
# add mentioned dependency

```     
        <dependency>
            <groupId>org.webjars</groupId>
            <artifactId>bootstrap</artifactId>
            <version>3.3.6</version>
        </dependency>
        <dependency>
            <groupId>org.webjars</groupId>
            <artifactId>jquery</artifactId>
            <version>1.9.1</version>
        </dependency>
        
  		
  
		<script src="webjars/jquery/1.9.1/jquery.min.js"></script>
	    <script src="webjars/bootstrap/3.3.6/js/bootstrap.min.js"></script>
		<link href="webjars/bootstrap/3.3.6/css/bootstrap.min.css"
	    		rel="stylesheet">
```
# @PostConstruct
The PostConstruct annotation is used on a method thatneeds to be executed after dependency injection is done to performany initialization. This method must be invoked before the classis put into service. This annotation must be supported on all classesthat support dependency injection. The method annotated with PostConstruct must be invoked even if the class doesnot request any resources to be injected. Only onemethod in a given class can be annotated with this annotation. 

Parsing a file means reading in a data stream of some sort and building an in memory model of the semantic content of that data.


# Survey 
# Differences between @RequestParam and @PathVariable annotations in Spring MVC?

As the name suggests, @RequestParam is used to get the request parameters from URL, also known as query parameters, while @PathVariable extracts values from URI.

The Spring MVC framework, one of the most popular frameworks for developing a web application in Java world also provides several useful annotations to extract data from the incoming request and mapping the request to the controller, e.g., @RequestMapping, @RequestParam, and @PathVariable. Even though both @RequestParam and @PathVariable is used to extract values from the HTTP request

For example, if the incoming HTTP request to retrieve a book on topic "Java" is 
# http://localhost:8080/shop/order/1001/receipts?date=12-05-2017, #

then you can use the @RequestParam annotation to retrieve the query parameter date and you can use @PathVariable to extract the orderId i.e. "1001" as shown below:

@RequestMapping(value="/order/{orderId}/receipts", method = RequestMethod.GET)
public List listUsersInvoices(@PathVariable("orderId") int order,
                              @RequestParam(value = "date", required = false) Date dateOrNull) {
...
}

The required=false denotes that the query parameter can be optional, but the URL must have the same URI.

What is REST?
Architectural style for the web. REST specifies a set of constraints.
Client - Server : Server (service provider) should be different from a client (service consumer).
Enables loose coupling and independent evolution of server and client as new technologies emerge.
Each service should be stateless.
Each Resource has a resource identifier.
It should be possible to cache response.
Consumer of the service may not have a direct connection to the Service Provider. Response might be sent from a middle layer cache.
A resource can have multiple representations. Resource can modified through a message in any of the these representations.


- Adding the second method to rest service to retrieve a specific question
- This will be a very short step
- http://localhost:8080/surveys/Survey1/questions/Question1
- Different Request Methods
  - GET - Retrieve details of a resource
  - POST - Create a new resource
  - PUT	- Update an existing resource
  - PATCH - Update part of a resource
  - DELETE - Delete a resource
  
 # public class ServletUriComponentsBuilder
extends UriComponentsBuilder
- UriComponentsBuilder with additional static factory methods to create links based on the current HttpServletRequest.

# static ServletUriComponentsBuilder	fromCurrentRequest()
- Same as fromRequest(HttpServletRequest) except the request is obtained through RequestContextHolder.
  
