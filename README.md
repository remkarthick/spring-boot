Spring Boot Quick Reference

# MVC - Model, View and Controller

- Model - Data needed by the View, represents the data. Its the data that the controller sends to the View
- View  - Skeleton, needs data to be meaningful, represents the visual elements of webpage. 
- Controller - Manages the model and Presents the view, sort of a connector. Handles the web request

## Annotations

* @Controller	- Converts a class to a controller. The Class now becomes entry point for all web requests. The class can now have handler methods
* @GetMapping	- Used to annotate a handler method for get
* @PostMapping	- Used to annotate a handler method for post
* @RequestParam

## Handler Method
Every handler method has access to the model passed as its function parameter.
ex. getGrades is a handler method. 
```
@GetMapping("/grades")
public String getGrades(Model model){
}
```
# Three Layer Architecture

Controller class --calls--> Service class  --calls--> Repository class

Old Method : Create an object of Service class in Controller class and Create an object of Repository class inside Service class

New Method : Instead of above, create a @Component of Service class and @Component of Repository class and @Autowired them instead of creating object

Note : Instead of using @Component use @Service/@Repository. All are same and creates Bean


* Repository class - Data Access Layer : CRUD Operations should be inside Repository class. It is the Data access layer. This should not communicate with the Controller class directly. Should use the Service class for communication with controller 
* Service class    - Business Layer : Business Logic layer. This is middle man between the Controller and Repository.
* Controller class - Presentation Layer (Model +View are here in this layer). Controllers only concern should be managing the model and presenting the view.

# Rest API


@ResponseBody - Serializes an Object into JSON, without this object will be returned as object and there will be error. Can be annotated at class level or handlerMethod level.

@PathVariable - To retrieve path variable
@RequestParam - To get query variables


ex. getGrades is a handler method. 
```
@GetMapping("/grades/{id}?name=Bingo")
@ResponseBody
public Grade getGrades(@PathVariable String id, @RequestParam String name){
  return new Grade("ABC",100); // this object will return as a JSON because we have the @ResponseBody annotation added
}
```

@RestController = @Controller + @ResponseBody

 - @RestController must be annotated at class level so all handler methods will serialize objects to json on return statement.

@ResponseEntity - instead of returning Object return it as a ResponseEntity

ex. getGrades is a handler method. 
```
@GetMapping("/grades/{id}")
@ResponseBody
public ResponseEntity<Grade> getGrades(@PathVariable String id){
  return new ResponseEntity<>(new Grade("ABC",100), HttpStatus.OK); 
}
```

@RequestBody - deserialize the request body json string to object

ex. postGrades is a handler method. 
```
@PostMapping("/grades/{id}")
@ResponseBody
public ResponseEntity<HttpStatus> postGrades(@PathVariable String id, @RequestBody Grade grade){
  gradeService.createGrade(grade);
 return new ResponseEntity<>(HttpStatus.CREATED); 
}
```
