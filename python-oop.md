# Object Oriented Programming 

| Procedural Programming | Object-oriented programming | 
| ---------------------- | --------------------------- |
| Sequential | Patterns | 
| Code as a sequence of steps | Code as interactions of objects | 
| Great for data analysis as scripts | Great for building frameworks and tools | 

# Fundamental OOP concepts 
## Objects as data structures 
  -   Object = state + behavior 
  -   **Ecapsulation** (another core tenant of OOP) = bundling data with methods that operate on it 
      -   For example, a customer as an object is made up of attributes, such as name, e-mail, phone number. Additionally the customer has actions she can take like place order, or cancel order. 
      
## Classes as templates
  - Classes are like a blueprint for an object. 
  - Classes incorporate information on objects' state and behavior 

    | Attributes | Methods | 
    | --------- | -------- |
    | State | Behavior | 
    | Variables (i.e. `my_obj.attribute`) | Functions (i.e. `my_obj.function()`)|
    
  - **Tip!** List all attributes and methods of an object by typing `dir(my_obj)`. Other helpful helper functions include `help(my_obj)` and `type(my_obj)`.

> **Note:** _Objects_ and _classes_ are related, but not the same. An _object_ is a representation or instance of a class, while a _class_ is a abstract blueprint or pattern for the methods and attributes of an object. 

### Methods
- _Method_ is the term used to reference function definition within a Class.

### Attributes
- _Attributes_ should be defined within a Class by assignment
- When referring to an attribute within a Class, use the syntax `self.attribute`

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

## `__init()__` constructor
- The `__init()__` contructor is a special method that can be defined within a Class, which initializes certain variables when an object is first instantiated. 
- This is also a good place to set default values for certain attributes
- The `__init()__` constructor is the preferred place (best practice) location within a Class to define all attributes. The benefits of defining all attributes here instead of individual _setter methods_, such as the `set_name()` method in the example above, include the following:
  -  Easier to read and maintain code due to all attributes being defined in a single location
  -  No need to worry about attempted to access attributes that have not been defined yet, leading to bugs and errors

    ![image](https://user-images.githubusercontent.com/2760319/137593198-1310bfad-c66e-4005-ba5d-2f5059ac7d2e.png)

### Example
```python
class Customer:
  """This is an example of a DocString, which is a large comment block explaining the Class"""
  def __init__(self, name, balance=0):
    self.name = name
    self.balance = balance
    print("The __init__ method was called")
```

# Best Practices for building a Class in Python
1. Define all attributes in the `__init__()` method
2. Use `CamelCase` for Class definition, and `snake_case` for method and attribute definitions
3. Keep `self` as `self`.
4. Use `docstrings`
