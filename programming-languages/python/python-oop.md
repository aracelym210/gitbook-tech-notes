# 🧱 OOP in Python

## Object Oriented Programming

| Procedural Programming             | Object-oriented programming             |
| ---------------------------------- | --------------------------------------- |
| Sequential                         | Patterns                                |
| Code as a sequence of steps        | Code as interactions of objects         |
| Great for data analysis as scripts | Great for building frameworks and tools |

## Fundamental OOP concepts

### Objects as data structures

* Object = state + behavior
* **Ecapsulation** (another core tenant of OOP) = bundling data with methods that operate on it
  * For example, a customer as an object is made up of attributes, such as name, e-mail, phone number. Additionally the customer has actions she can take like place order, or cancel order.

### Classes as templates

* Classes are like a blueprint for an object.
*   Classes incorporate information on objects' state and behavior

    | Attributes                          | Methods                              |
    | ----------------------------------- | ------------------------------------ |
    | State                               | Behavior                             |
    | Variables (i.e. `my_obj.attribute`) | Functions (i.e. `my_obj.function()`) |
* **Tip!** List all attributes and methods of an object by typing `dir(my_obj)`. Other helpful helper functions include `help(my_obj)` and `type(my_obj)`.

> **Note:** _Objects_ and _classes_ are related, but not the same. An _object_ is a representation or instance of a class, while a _class_ is a abstract blueprint or pattern for the methods and attributes of an object.

#### Methods

* _Method_ is the term used to reference function definition within a Class.

#### Attributes

* _Attributes_ should be defined within a Class by assignment
* When referring to an attribute within a Class, use the syntax `self.attribute`

## Writing a class

### `self` argument in class methods

* Adding a method, or function, to a class is written in the same format a method is written outside of a class definition. The biggest exception to this is the use of the `self` argument
* `self` is a stand-in for a future object used in class definition.
*

#### Template

```python
class <Class_name>:
  
  def method(self, arg_two, arg_n):
    pass
```

#### Example

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

### `__init()__` constructor

* The `__init()__` contructor is a special method that can be defined within a Class, which initializes certain variables when an object is first instantiated.
* This is also a good place to set default values for certain attributes
*   The `__init()__` constructor is the preferred place (best practice) location within a Class to define all attributes. The benefits of defining all attributes here instead of individual _setter methods_, such as the `set_name()` method in the example above, include the following:

    * Easier to read and maintain code due to all attributes being defined in a single location
    * No need to worry about attempted to access attributes that have not been defined yet, leading to bugs and errors

    ![image](https://user-images.githubusercontent.com/2760319/137593198-1310bfad-c66e-4005-ba5d-2f5059ac7d2e.png)

#### Example

```python
class Customer:
  """This is an example of a DocString, which is a large comment block explaining the Class"""
  def __init__(self, name, balance=0):
    self.name = name
    self.balance = balance
    print("The __init__ method was called")
```

## Best Practices for building a Class in Python

1. Define all attributes in the `__init__()` method
2. Use `CamelCase` for Class definition, and `snake_case` for method and attribute definitions
3. Keep `self` as `self`.
4. Use `docstrings`

## Instance and Class Data

* **Inheritance:** Extends functionality of existing code
* **Polymorphism:** Creates a unified interface
* **Encapsulation:** Bundling of data and methods

### Instance-level data

* Data bound by `self` to bind to a particular instance.
* Example:
  * Instance level varibales defined in `__init__()` method with instance level attributes (i.e. `self.name`, `self.salary`)

### Class-level data

* Data shared among all instances of a class

#### Class attributes

* _Class attributes_ are defined directly in the body of `class`, outside of any methods or constructors. They are "global variables" within the class

> **When to use?** class-level attributes are used when you want certain data/ attributes/ variables to be shared among all Class objects. For example, a minimum salary in the example of the employee class, should not change between each instance of the employee class. Other possible usecases for class attributes include min/max values for attributes and commonly used values and constants

**Example**

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

#### Class methods

* Class methods cannot use instance-level data

> **When to use?** The main usecase of useage of a class methods is "alternative constructors." You might want to create a class method when there are multiple ways to intialize, such as from an external reference file.

* Special syntax of class methods include
  * The **"class method decorator"** `@classmethod`
  * The first argument of a class method is `cls` instead of `self` like other methods within a class.
  * To call a class method, use `ClassName.method()` syntax instead of `object.method()`

**Example**

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

## Inheritance

* A core concept of OOP

#### Example

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

### Customizing functionality via inheritance

* Add methods as usual
* Can use data from both parent and child class

#### Example

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

## Operator overloading: comparison

### Comparison operators

| Operator | Method     |
| -------- | ---------- |
| `==`     | `__eq__()` |
| `!=`     | `__ne__()` |
| `>=`     | `__ge__()` |
| `<=`     | `__le__()` |
| `>`      | `__gt__()` |
| `<`      | `__lt__()` |

* creating two objects of the same class, with the same data, will return as `False` if you attempt to check if they are equal to each other. This is because the variable that is storing the class object is just storing a _reference point to the memory location_ where the data is stored.
* After overloading the `__eq__()` constructor with the example code from below, comparing two objects that share the same values will return an expected outcome

#### Example - Overloading **eq**()

```python
class Customer:
  def __init__(self, id, name, balance):
    self.id = id
    self.name = name
    self.balance = balance
    
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
  
  def __str__(self):
    cust_str = """
    Customer: 
      name: {name}
      balance: {balance}
   """.format(name = self.name \ 
              balance = self.balance)
   return cust_str
   
  #  if __str__() was not defined, print() would default to __repr__()
  def __repr__(self):
    return "Customer({id}, '{name}', {balance})".format(id = self.id, name = self.name, balance = self.balance)
```

* When using our overloaded **eq**() method, it's a good idea to add a check to make sure the objects that are being compared are the same type of Class.
* Python always calls the child's **eq**() method when comparing a child object to a parent object.
* You should always define at least one of the string representation methods (`__str__()` or `__repr__()` for your object to make sure that the person using your class can get important information about the object easily.

### More methods to overload in a Class object

| Method       | Usecase                                                               |
| ------------ | --------------------------------------------------------------------- |
| `__str__()`  | executed when `print()` is called on an object. Considered "informal" |
| `__repr__()` | executed when `repr()` is called. Mainly used by developers.          |

## Exceptions and Exception handling

* `try` - `except` - `finally`
* Exceptions are classes. See [Python documentation for more information](https://docs.python.org/3/library/exceptions.html)
  * standard exceptions inherited from `BaseException` or `Exception`

#### Raising exceptions

* Sometimes we may want to have more control over the errors that may arise when our code is being used. This is what the `raise` keyword is for.
* `raise ExceptionNameHere('Error message here')`
* The user of the code can then handle the error using `try / except` blocks

#### Custom exceptions

* To define a custom Exception, create a class that inherits from the `Exception Class` or one of the subclasses

```python
class BalanceError(Exception): pass 

class Customer:
  def __init__(self, name, balance):
    if balance < 0: 
      raise BalanceError("Balance has to be non-negative!")
    else:
      self.name, self.balance = name, balance 
     
```

#### Parent/ child Exception classes (inheritance)

* It's better to include an except block for a child exception before the block for a parent exception, otherwise the child exceptions will be always be caught in the parent block, and the except block for the child will never be executed.

## Designing for Inheritance and Polymorphism

* When designing a Class, principles and best practices regarding inheritance and polymoprphism should come to mind
* _Polymorphism_: Using a unified interface to operate on objects of different classes (think, subclasses).
  * Example: `class BankAccount:` and two classes that inherit from `BankAccount` - `class CheckingAccount(BankAccount):` and `class SavingsAccount(BankAccount):`. Instead of having two `account_withdraw()` methods in each subclass, one method can be defined in BankAccount class, thus providing a unified interface to operate on different banking class objects.
*   The _**Liskov substitution principle**_ is a fundamental oop design princple that provides guidance on _when and how_ to use inheritance properly. Named after Computer Scientist, Barbara Liskov.

    > "Base class should be interchangable with any of it's subclasses without altering and properties of the program."

    * Liskov substitution princple (LSP) should be true both
      * **Syntactically**: Methods in the subclass should have a signature with parameters and returned values compatible with the method in the parent class.
      * **Semantically** The state of objects also must stay consistent; the subclass method shouldn't rely on stronger input conditions, should not provide weaker output conditions, it should not throw additional exceptions and so on.
    * Example: Anywhere a `BankAccount` object is used, we should be able to change that object to a `CheckingAccount` object and not have to change any properties of the code. It should work as is.

### Violations of Liskov Substitution Principle (LSP)

**Syntactic incompatability**

* `BankAccount.withdraw()` requires 1 parameter but `CheckingAccount.withdraw()` requires two. Thus, we could not substitute the parent class for the child class.

**Subclass strengthenting input conditions**

* `BankAccount.withdraw()` accepts any amount but `CheckingAccount.withdraw()` assumes that the amount is limited

**Subclass weakening output conditions**

* `BankAccount.withdraw()` can only leave a positive balance or throw an error, but `CheckingAccount.withdraw()` can have a negative balance

**Changing additional attributes in a subclass method** **Throwing additional exceptions in a subclass that the base class does not throw**

### Cicle-ellipse problem

* The [circle-ellipse problem](https://en.wikipedia.org/wiki/Circle%E2%80%93ellipse\_problem) is a classic example in software development, that illustrates a violation of the LSP. This is sometimes called the square-rectangle problem.
