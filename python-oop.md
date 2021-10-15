# Object Oriented Programming 

| Procedural Programming | Object-oriented programming | 
| ---------------------- | --------------------------- |
| Sequential | Patterns | 
| Code as a sequence of steps | Code as interactions of objects | 
| Great for data analysis as scripts | Great for building frameworks and tools | 

# Fundamental OOP concepts 
- **Objects** as data structures 
  -   Object = state + behavior 
  -   **Ecapsulation** (another core tenant of OOP) = bundling data with code operating on it 
      -   For example, a customer as an object is made up of attributes, such as name, e-mail, phone number. Additionally the customer has actions she can take like place order, or cancel order. 
- **Classes** 
  - Classes are like a blueprint for an object. 
  - Classes incorporate information on objects' state and behavior 

    | Attributes | Methods | 
    | --------- | -------- |
    | State | Behavior | 
    | Variables (i.e. `my_obj.attribute`) | Functions (i.e. `my_obj.function()`)|
    
  - **Tip!** List all attributes and methods of an object by typing `dir(my_obj)`. Other helpful helper functions include `help(my_obj)` and `type(my_obj)`.

> **Note:** _Objects_ and _classes_ are related, but not the same. An _object_ is a representation or instance of a class, while a _class_ is a abstract blueprint or pattern for the methods and attributes of an object. 

# Writing a class
### Template
```python
class <Class_name>:
  # class code goes here 
```
### Example
```python
class Customer:
  # code for class goes here
  pass
  
c1 = Customer()     # Class_name() creates an object of the class Class_name. In this case, Customer ()
c2 = Customer()
```
