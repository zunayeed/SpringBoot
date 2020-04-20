 
  1.  create a LoginController class
  2.  create a method to map request(/login) 
  3.  add annotation to class(@Controller) and method (@RequestMapping  @ResponseBody )
  4.  Create a link list-todos in the welcome jsp page 
  5.  Create a TodoController class with @Controller annotation. It needs TodoService 
  	* create a TodoService with @Autowired annotation: @Autowired TodoService Service
	     - import TodoService
	 * to configure the mapping of /list-todos web reruest, map it to a method with 
	    @RequestMapping(value="/list-todos, method = RequestMethod.GET) 
	 * using model.put(), retrieve  service.retrieveTodos()
	     model.put("todos", service.retrieveTodos("zunayeed"));
	 * create list-todos.jsp  with  ${todos}
  6.  Create a TodoService class with @Service annotation. @Service  used for business logic 
  7.  Add `@SessionAttributes("name")` annotation in LoginController class and TodoController class, and it will make the name available to all subsequest classes(a way of storing values across multiple classes - Session) . 
       * Add this line inside  showTodos() of TodoController class
      ` String name =  (String)model.get("name");`
      `model.put("todos", service.retrieveTodos(name)); `
  
  
  8. 
  Add the link below in head tag 
  `<link href="webjars/bootstrap/3.3.6/css/bootstrap.min.css"
	    		rel="stylesheet">`


   * Add link belw in end of body tag: 
   
             `<script src="webjars/jquery/1.9.1/jquery.min.js"></script>
	     <script src="webjars/bootstrap/3.3.6/js/bootstrap.min.js"></script>`
	     
9.  in list todo.jsp  for validation 

``` 
	<form method="post">
	<fieldset class="form-group">
		<label>Description</label>
		<input name="desc" type="text" class="form-control" required="required"/>
	</fieldset>
		
       <button type = "submit" class ="btn btn-succss" >Add</button>/>
       </form>
```

10. 
   *   Update todo controller and add tag libtary
- Command Bean or Form Backing Bean: use of bean instrad of requestparam : 
Inorder to use comand bean, two things need to be done: 
aController
b View - Spring Form Tags
-  Purpose: you want to get add user infor as part of todo object we use command bean
- Add Validations
- The JSR 303 and JSR 349 defines specification for the Bean Validation API (version 1.0 and 1.1, respectively), and Hibernate Validator is the reference implementation.
- org.hibernate:hibernate-validator
 In summary: 
   instead of @requestparam, use Todo to and in the body use todo.getDesc()
   
  11  in jsp change name attribute  to path 
     and add form tag in form  label 
     also use modelAttribute
   path attribute is usee to access variable directly from java 
