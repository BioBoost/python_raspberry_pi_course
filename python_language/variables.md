## Variables

Application need to store all sorts of data. From simple things such as numbers, characters and string to complex data types that a programmer can define for himself.

This data is stored, manipulated and outputted through the application. The data itself is stored inside the memory of the computer or system the program is running on. Inside your application you do not need to access the memory directly, for this you can make use of variables.

A variable is a **symbolic name** for information. The variable's name should represent what information the variable contains. They are called variables because they represent *information that can change*.

Computer memory can be thought of a huge cabinet with millions of small drawers. The content of the drawers is the information
stored in memory that we use inside our application. While it would be possible to refer to a drawer using its location (for example
second row, third column), it is a lot harder to remember. There is also no link between the location and the actual content of the drawer.
Now if we place a label on the drawer that is descriptive enough of its content, which is the analogy of our variable name, it is much easier to refer to the drawer using the descriptive name (for example nine inch nails).

![Memory is analogous to a huge cabinet with millions of small drawers](img/drawers_memory.png)

You may actually have already been using variables for quite a while. When doing math you also use symbolic names for variables. For example

```text
x = 15
y = 13

p = x * y
```

Or when defining a linear equation

```text
y = f(x) = ax + b
```

### Declaring a variable

Compared to languages such as C++ and Java, Python is a dynamic typed language. This means that we do not have to define a variable and its type before using it. Python is pretty smart when it comes to variables as it interprets and declares variables when they are being set equal to a value. It also automatically determined the type of the variable based on the value assigned to it.

The type of the variable determines the size and layout of the variable's memory; the range of values that can be stored within that memory; and the set of operations that can be applied to the variable.

Let's take a look at an example where a variable `numberOfStudents` is assigned an integral value to store the number of students in the classroom. Based on the integral value assigned to the variable Python knows it should store the value as an integer. Next the result can be printed to the terminal. When you wish to use the content of the variable, all you need to do is state the symbolic name where you would otherwise
use a value.

```Python
# Storing the number of students in the classroom
numberOfStudents = 31

# Print age
print(age)
```

The variable can be assigned a value or changed using the **assignment operator** `=`. This is basically the same as in
math. On the left hand side you have the variable name which you want to assign and on the right hand side the value.

If you wish to place a text string before the value of `numberOfStudents` you can use the string concatenation operator `+` when passing the data to the `print` function. Do note that you need to explicitly tell Python to convert the integral `numberOfStudents` value to a string by passing `numberOfStudents` to the `str()` function as shown in the code below:

```Python
# Storing the number of students in the classroom
numberOfStudents = 31

# Print with concatenation
print("Our current course has " + str(numberOfStudents) + " students attending it.")
```

The assignment operator can also be used to assign one variable's value to another.

```Python
# Storing the number of students in the classroom
numberOfStudents = 31
numberOfOccupiedChairs = numberOfStudents

# Print with concatenation
print("Our current course has " + str(numberOfStudents) + " students attending it.")
print("This means that there are " + str(numberOfOccupiedChairs) + " seats taken.")
```

Of course if you want to use the value of a variable in an expression or statement the variable must exist. If it doesn't then Python will generate an error like:

```text
Traceback (most recent call last):
  File "C:\Users\nicod\Desktop\test.py", line 9, in <module>
    notAnExistingVariable
NameError: name 'notAnExistingVariable' is not defined
```
