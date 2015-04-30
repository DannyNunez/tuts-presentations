Placing functional code in the global name is never a good idea. It can cause collisions that are hard to debug. 

- In Angular a module is a the main way to define an Angular js App. 
- The module of an application is where we will contain all of our application code. 
- An app can contain several modules , each one containing ode that pertains to specific functionality. 

#### Advantages of modules

- Keeps global namespace clean. 
- make tests easier to write. 
- keeps test clean 
- easily target code for testing 
- isolated functionality

#### Angular Module API 

````

angular.module('myApp', []);

````

