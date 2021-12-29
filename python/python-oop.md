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

# Instance and Class Data
- __Inheritance:__ Extends functionality of existing code 
- __Polymorphism:__ Creates a unified interface
- __Encapsulation:__ Bundling of data and methods 

## Instance-level data
- Data bound by `self` to bind to a particular instance. 
- Example: 
  - Instance level varibales defined in `__init__()` method with instance level attributes (i.e. `self.name`, `self.salary`)

## Class-level data
- Data shared among all instances of a class 

### Class attributes 
- _Class attributes_ are defined directly in the body of `class`, outside of any methods or constructors. They are "global variables" within the class
> __When to use?__ class-level attributes are used when you want certain data/ attributes/ variables to be shared among all Class objects. For example, a minimum salary in the example of the employee class, should not change between each instance of the employee class. Other possible usecases for class attributes include min/max values for attributes and commonly used values and constants 

#### Example
```python
class Employee:
  MIN_SALARY = 30000      # self. is not used for class attributes

  def __init__(self, name, salary):
    self.name = name

    # Use class name to access class attribute
    if salary >= Employee.MIN_SALARY:
      self.salary = salary
    else:
      self.salary = Employee.MIN_SALARY
```

### Class methods
- Class methods cannot use instance-level data
> __When to use?__ The main usecase of useage of a class methods is "alternative constructors." You might want to create a class method when there are multiple ways to intialize, such as from an external reference file.
- Special syntax of class methods include
  - The __"class method decorator"__ `@classmethod`
  - The first argument of a class method is `cls` instead of `self` like other methods within a class.
  - To call a class method, use `ClassName.method()` syntax instead of `object.method()`

#### Example
```python
class Employee:
  MIN_SALARY = 30000      # self. is not used for class attributes

  def __init__(self, name, salary):
    self.name = name

    # Use class name to access class attribute
    if salary >= Employee.MIN_SALARY:
      self.salary = salary
    else:
      self.salary = Employee.MIN_SALARY

  @classmethod
  def from_file(cls, filename):     # self is not passed in classmethods
    with open(filename, "r") as f:
      name = f.readline()

    return cls(name)                # cls() will call the __init__() constructor
```

# Inheritance
- A core concept of OOP

### Example
```python
class Employee:
  MIN_SALARY = 30000    

  def __init__(self, name, salary=MIN_SALARY):
      self.name = name
      if salary >= Employee.MIN_SALARY:
        self.salary = salary
      else:
        self.salary = Employee.MIN_SALARY
  def give_raise(self, amount):
    self.salary += amount      
        
# MODIFY Manager class and add a display method
class Manager(Employee):
  def display(self):
    print("Manager " + self.name)

mng = Manager("Debbie Lashko", 86500)
print(mng.name)

# Call mng.display()
mng.display()
```

**Output**
```
Debbie Lashko
Manager Debbie Lashko
```

## Customizing functionality via inheritance
- Add methods as usual
- Can use data from both parent and child class

### Example 
```python 
# class SubClassName(InheritedParentClassName)
class CheckingAccount(BankAccount):

  # customized constuctor that also executes parent code
  def __init__(self, balance, limit):
    BankAccount.__init__(self, content)
    self.limit = limit
    
   def deposit(self, amount): 
    self.balance += amount
    
   def withdraw(self, amount, fee=0):
    if fee <= self.limit:
      BankAccount.withdraw(self, amount - fee)
    else: 
      BankAccount.withdraw(self, amount - self.limit)

```

# Operator overloading: comparison
- creating two objects of the same class, with the same data, will return as `False` if you attempt to check if they are equal to each other. This is because the variable that is storing the class object is just storing a _reference point to the memory location_ where the data is stored. 
- After overloading the `__eq__()` constructor with the example code from below, comparing two objects that share the same values will return an expected outcome

### Example - Overloading __eq__()
```python
class Customer:
  def __init__(self, id, name):
    self.id, self.name = id, name
    
  # Will be called when == is used
  def __eq__(self, other):
    $Diagnostic printout
    print("__eq__() is called.")
    
    #  Check that objects are the same type of Class
    if type(self) == type(other):
      return (self.id == other.id) and \
             (self.name == other.name)
    else:
      return False
```
- When using our overloaded __eq__() method, it's a good idea to add a check to make sure the objects that are being compared are the same type of Class. 
- Python always calls the child's __eq__() method when comparing a child object to a parent object.
