# Object Oriented Programming 

| Procedural Programming | Object-oriented programming | 
| ---------------------- | --------------------------- |
| Sequential | Patterns | 
| Code as a sequence of steps | Code as interactions of objects | 
| Great for data analysis as scripts | Great for building frameworks and tools | 

# Fundamental OOP concepts 
- **Objects** as data structures 
  -   Object = state + behavior 
  -   **Ecapsulation** (another core tenant of OOP) = bundling data with methods that operate on it 
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
## `self` argument in class methods
- Adding a method, or function, to a class is written in the same format a method is written outside of a class definition. The biggest exception to this is the use of the `self` argument 
- `self` is a stand-in for a future object used in class definition. 
- 
### Template
```python
class <Class_name>:
  
  def method(self, arg_two, arg_n):
    pass
```
### Example
```python
class Customer:
  # set the name attribute of an object to new_name
  def set_name(self, new_name):
    self.name = new_name          # will create .name (attribute) when set_name is called 
    
  def identify(self):
    print("I am customer " + self.name)
  
c1 = Customer()     # Class_name() creates an object of the class Class_name. In this case, Customer ()
c2 = Customer()
```
