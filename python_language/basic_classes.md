# Basic Classes in Python

Classes provide a means of bundling data and functionality together.

Python has been an object-oriented language from the beginning. Because of this, classes and object have been integrated deeply into the language. Creating classes and objects from those classes are very easy. This chapter expects you to have a basic knowledge of OOP and its concepts. However, following is a small overview of the most important terminology and concepts.

* A **class** a user-defined prototype for an object that defines a set of attributes that characterize any object of that class. The attributes are data members (class variables and instance variables) and methods, accessed via dot notation `object.method()`.
* A **class variable** is shared by all instances of a class. Class variables are defined within a class but outside any of the class's methods. Class variables are not used as frequently as instance variables are.
* An **instance** is an individual object of a certain class. An object that has been created from a class Circle, for example, is an instance of the class Circle.
* An **instance variable** is a variable that is defined inside a method and belongs only to the current instance of that class, the object in other words.
* **Instantiation** is the creation of an object of a class.
* A **method** is a kind of function that is defined in a class definition. The methods belonging to the class define the **behavior** of the objects of that class.
* An **object** is a unique instance of a data structure that is defined by its class. An object comprises both data members (class variables and instance variables) and behavior (methods).
* **Method overloading** is the assignment of more than one behavior to a particular method. The operation performed varies by the types of objects or arguments involved.
* **Inheritance** is the extension of existing classes with new data and/or behavior.

## Creating Classes

To create a class, one can follow the syntax shown below:

```python
class <NameOfClass>:
  """Descriptive string of class function"""

  # Methods ...
```

The `class` keyword is mandatory and so is the name of the class. Naming classes in Python follows Camel Case convention.
<!-- TODO: Descriptive string explanation -->

### Methods

Adding functionality to a class in the form of methods is achieved using the `def` keyword and the template shown below:

```python
class <NameOfClass>:
  """Descriptive string of class function"""

  # Methods ...
  def <name_of_method>(self, <arguments>):
    # Statements ...
```

The `self` keyword is implicitly populated with the object the method is called on, however when defining the method inside the class it needs to be explicitly noted as the first argument. The rest of the arguments are the data that the creator of the class requires for the method to do its processing.

#### Constructor

A special method is the constructor which is responsible for delivering a valid object when the user of the class request the creation of a new instance. This method has the mandatory name `__init__`. Based on your requirements you can pass arguments to the object's constructor.

```python
class <NameOfClass>:
  """Descriptive string of class function"""

  # Constructor
  def __init__(self, <arguments>):
    # Initialize object

  # Methods ...
  def <name_of_method>(self, <arguments>):
    # Statements ...
```

Compared to many other programming languages Python does not allow you to create multiple constructors (constructor overloading).

### Creating Objects from a Class

Creating objects from a class in Python uses function notation. Just pretend that the class object is a parameterless function that returns a new instance of the class (actually the constructor method is implicitly called).

```python
obj = NameOfClass()
```

### Instance Variables or Attributes

To assign or access attributes of the class you need to make use of the dot-notation on the `self` keyword. As with variables, in Python one does not need to declare attributes before using them.

```python
class <NameOfClass>:
  """Descriptive string of class function"""

  # Constructor
  def __init__(self, <arguments>):
    # Initialize object

  # Methods ...
  def <name_of_method>(self, <arguments>):
    # Statements ...
    self.<name_of_attribute> = <value>
```

### Returning Values from Methods

Methods can also return a single value using the `return` keyword. In this case the code that calls the method can assign the return value to a variable.

```python
  # Method that returns a value
  def <name_of_method>(self, <arguments>):
    return <some_value>
```

### Example

Let us put all of this into practice and create a class `Robot`.

```python
class Robot:
  """Class that models a talking robot"""

  # Constructor with no arguments
  def __init__(self):
    # Here we set the name argument
    # as an attribute of the object
    self.name = "Nameless"

  def say_hello(self):
    # We can access the name attribute via the
    # self reference and the dot-operator
    print("Hello I am " + self.name)

  # Method allows us to rename the robot
  # @name: name of the robot
  def set_name(self, name):
    self.name = name

  def get_name(self):
    return self.name
```

When creating a Robot we need to save the object in a variable:

```python
# Create a Robot object
myRobot = Robot()

# Call a method on the Robot object
myRobot.say_hello()

# Rename the robot
myRobot.set_name("Pokey")
myRobot.say_hello()

name = myRobot.get_name()
print("The robot is called " + name)
```

To test this out you can just add the class definition of `Robot` to a Python script and place the instantiation code below it as shown here:

```python
class Robot:
  """Class that models a talking robot"""

  # Constructor with no arguments
  def __init__(self):
    # Here we set the name argument
    # as an attribute of the object
    self.name = "Nameless"

  def say_hello(self):
    # We can access the name attribute via the
    # self reference and the dot-operator
    print("Hello I am " + self.name)

  # Method allows us to rename the robot
  # @name: name of the robot
  def set_name(self, name):
    self.name = name

  def get_name(self):
    return self.name

# Create a Robot object
myRobot = Robot()

# Call a method on the Robot object
myRobot.say_hello()

# Rename the robot
myRobot.set_name("Pokey")
myRobot.say_hello()

name = myRobot.get_name()
print("The robot is called " + name)
```

Which outputs:

```text
Hello I am Nameless
Hello I am Pokey
The robot is called Pokey
```
