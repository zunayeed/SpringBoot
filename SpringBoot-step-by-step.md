 
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
	6.   Create a TodoService class with @Service annotation. Service class contains business logic 
  7.  Add `@SessionAttributes("name")` annotation in LoginController class and TodoController class, and it will make the name available to all subsequest classes(a way of storing values across multiple classes - Session) . 
       * Add this line inside  showTodos() of TodoController class
      ` String name =  (String)model.get("name");`
		  `model.put("todos", service.retrieveTodos(name)); `
