Question: what is @SpringBootApplication annotation ? 
Many Spring Boot developers like their apps to use 
         -auto-configuration, 
         -component scan and
         -be able to define extra configuration on their "application class".
         
         A single @SpringBootApplication annotation can be used to enable those three features, that is:

@EnableAutoConfiguration: enable Spring Boot’s auto-configuration mechanism
@ComponentScan: enable @Component scan on the package where the application is located 
@Configuration: allow to register extra beans in the context or import additional configuration classes

The @SpringBootApplication annotation is equivalent to using @Configuration, @EnableAutoConfiguration, and @ComponentScan with their default attributes, as shown in the following example:

package com.example.myapplication;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication // same as @Configuration @EnableAutoConfiguration @ComponentScan
public class Application {

	public static void main(String[] args) {
		SpringApplication.run(Application.class, args);
    
    In summary, @SpringBootApplication initalizes Spring(ComponentScan) and SpringBoot(AutoConfiguration).
    
    >>>   SpringApplication.run launches a Springboot application
    
    
    Step 2: 
@RequestMapping(value = "/login", method = RequestMethod.GET)
http://localhost:8080/login
Question:  Why @ResponseBody?
Answer:  @ResponseBody
The @ResponseBody annotation tells a controller that the object returned is automatically serialized into JSON and
 passed back into the HttpResponse object.
Important of RequestMapping method
How do web applications work? Request and Response
Browser sends Http Request to Web Server
Code in Web Server => Input:HttpRequest, Output: HttpResponse
Web Server responds with Http Response

----------------------------------------------------------------------------------------------------------------------
spring is popular because 
	          1) it enables writing testable codes
	           enables to write good unit test so easily
	          2) no plumbing code: trycatch block, lots of line of code, but in spring it is almost nothin
          	3) Architectural flexibility: strong modular concept 
            4) Follows current trend: spring boot helps develpo microservices very easily

Maven is used to manage the dependency of Java projects 

Springboot is one of the popular spring framework to develop micro services.
Group Id: package name 
Artifact Id: class name

SpringApplication.run launches a Springboot Application

spring-boot-starter-parent has all default configuration of all important maven dependencies

Spring Boot Starter Web provides: 1) all dependies to run web applications: core, mvc, validation,login 
Dev tools helps developer in saving time

MVC: 
1)  when dispatcher servlet sees that a request is coming to  /login, it sends the request to it sends the request to LoginController's loginMessage method because /login is mapped to it. 

    dispatcher servlet gets this login, and due to @ResponseBody, dispatcher servlet will directly return this content to the browser.

      dispatcherServlet does not know the path of login.jsp. It search for a view named "login".

     HOW do we let dispatcherServlet know that this view is in this specific path:
      login.jsp path:  /src/main/webapp/WEB-INF/jsp/login.jsp . 


> 	now the view resolver concept comes into picture
		whenever controller return login, it need to map in to specific login.jsp file.  
		"login"  =>  /src/main/webapp/WEB-INF/jsp/login.jsp 
  in spring, we use application.properties, by using a view resolver
		Second Snippet - /src/main/resources/application.properties

		spring.mvc.view.prefix: /WEB-INF/jsp/
		spring.mvc.view.suffix: .jsp
		logging.level.: DEBUG
but still we do not see the jsp page
     Third Snippet : To enable jsp support in embedded tomcat server!
inorder to add jsp support for the tomcat jsp server, we added the tomcat-embed-jasper dependency in the pom.xml file. 

        <dependency>
            <groupId>org.apache.tomcat.embed</groupId>
            <artifactId>tomcat-embed-jasper</artifactId>
            <scope>provided</scope>
        </dependency>
but still no update, because springboot developer tools can only handle changes within the application. when we change pom.xml, we are changing the dependency, or jar files. in this kind of situation we need to restart the whole application



   	server.port=8082
	spring.mvc.view.prefix=/jsp/
	spring.mvc.view.suffix=  .jsp
	logging.level.org.springframework.web: DEBUG

> when we pass variable to chrome address bar in login, how does it go to controller ? at controller, we use @RequestParam annotation, so we want to bind the request parameter, in import it is web.bind.annotation.RequestParam
   get request > controller > view 
then it shows the result in the console, not in jsp view. in order to make it available to view, in spring mvc we use model .




 Model is used to pass data from controller to view (JSP). So, we need to put the data in the model so that we can pass it to the view. 

So the controller controls the entire flow, once it has some data, it puts it to the model, and redirects it to the view. The view uses the model to render the data. 

So once the name through the @RequestParam annotation comes into the controller, we need to put it in model. In order to put it in model, we  need to have ModelMap object passed in to the method parameter. in model.put parameter we mention the attribute and value. So whatever you mention in the put, it will be available in the jsp. So, in order to access the value of variable in JSP, we use expression language ${<variable_name>}

Any request that comes to web application, it comes to the front controller. 

                                                     Spring MVC Request Flow: 
1)DispatcherServlet receives HTTP Request.
2) DispatcherServlet identifies the right Controller based on the URL.
3)Controller executes Business Logic.
4)Controller returns a) Model b) View Name Back to DispatcherServlet.
5)DispatcherServlet identifies the correct view (ViewResolver).
6)DispatcherServlet makes the model available to view and executes it.
7)DispatcherServlet returns HTTP Response Back.

    Flow : http://docs.spring.io/spring-framework/docs/2.0.8/reference/images/mvc.png


view resolver maps logical name to a physical jsp 

get method is not secure, we can see data in the url. in internet data travels from router to router, so data can be seen easily. So the ideal solution is using post. 


                                                  Annotation used in bean: 
1)@Component to create bean
2)@Service is used for business logic
3)@Repository for storing data to database, JPA
4)@Controller - if bean handle request from browser
5)@Autowired - to declare dependent componet of bean, 
6)@ComponentScan @SpringbootApplication has componenscan builtin - spring search component within the package

Spring framework is all about finding your component and autowiring components. 

If you want to store something across multiple pages, then session comes into picture.

-------------------------------------------------------------------------------------------------------------

when user types /login. we want to send them back "Hello world"

the way we do : 
  1) create a login controller class
  2) create a method to map request(/login) 
  3) add annotation to class(@Controller) and method (@RequestMapping  @ResponseBody )
  
  
                 
                 
                 
                                    Code To Demonstrate : 
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







>>>>      To see spring level debug: 
                                     src/main/resources/application.properties
                                      logging.level.org.springframework.web: DEBUG

                              4  What You Will Learn during this Step:
Your First JSP
There is a bit of setup before we get there!
Introduction to View Resolver
Useful Snippets and References
  1) Set up login.jsp file : 
First Snippet - /src/main/webapp/WEB-INF/jsp/login.jsp

<html>
<head>
<title>Yahoo!!</title>
</head>
<body>
My First JSP!!!
</body>
</html>
2) add dependency to application.properties file 
Second Snippet - /src/main/resources/application.properties

spring.mvc.view.prefix: /WEB-INF/jsp/
spring.mvc.view.suffix: .jsp
logging.level.: DEBUG

3) to enable jsp support, add the dependency
Third Snippet : To enable jsp support in embedded tomcat server!

        <dependency>
            <groupId>org.apache.tomcat.embed</groupId>
            <artifactId>tomcat-embed-jasper</artifactId>
            <scope>provided</scope>
        </dependency>
        
        
        
        
                              5 What You Will Learn during this Step:
You first GET Parameter.
Problem with using GET
Snippets
ModelMap model
model.put("name", name);
My First JSP!!! My name is ${name}

          >>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>
     
  Question:  What is @RequestParam in spring?
Answer: 
       Spring MVC RequestParam Annotation:  In Spring MVC, the @RequestParam annotation is used to read the form data and bind it automatically to the parameter present in the provided method. So, it ignores the requirement of HttpServletRequest object to read the provided data.
       
 >>>>>>>> Model is used to pass data from controller to view(JSP).  
       So, we need to put the data in the model so that we can pass it to the view. So the controller controls the entire flow, once it has some data, it puts it to the model, and model redirects it(data) to the view. The view uses the model to render the data. 

So, once the data(String name) -through the @RequestParam annotation- comes into the controller, we need to put it in model. In order to put it in model, we  need to have ModelMap object(ModelMap model) passed in to the method parameter.


In model.put("name", value)  we mention the attribute and value as name of parameter as name. 

So whatever you mention in the model.put("name", value), it will be available in the jsp. So, in order to access the value of variable in JSP(login.jsp) , we use expression language ${<variable_name>} ${name}

In brief 
 a ) the steps in controller
 
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

b) file is in jsp: 

                          src/main/webapp/WEB-INF/jsp/login.jsp
<html>
<head>
<title>Welcome to Login Portal</title>
</head>
<body>
Welcome to Simple login portal 
Here you will get value from model ${name}
</body>
</html>



.................>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>

                                           Spring MVC Request Flow
DispatcherServlet receives HTTP Request.
DispatcherServlet identifies the right Controller based on the URL mapping
Controller executes Business Logic.and puts data into model 
Controller returns a) Model b) View Name Back to DispatcherServlet.
DispatcherServlet identifies the correct view (ViewResolver).
Viewresolver maps logical name to physical jsp using the help from application.properties file.
        spring.mvc.view.prefix: /WEB-INF/jsp/
        spring.mvc.view.suffix: .jsp
DispatcherServlet makes the model available to view and executes it.
DispatcherServlet returns HTTP Response Back.
Flow : http://docs.spring.io/spring-framework/docs/2.0.8/reference/images/mvc.png

    
    
