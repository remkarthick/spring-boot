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
