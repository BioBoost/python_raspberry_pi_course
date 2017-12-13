## Lists

A basic data structure in Python is the list. In a list the elements are stored sequentially and accessible via a positional number called the index. The first index is zero, the second index is one, and so forth.

There are certain things you can do with lists such as indexing, slicing, adding, multiplying, .... In addition, Python has built-in functions for finding the length of a list and for finding its largest and smallest elements.

Only the basic operations are discussed further in this course as otherwise they would lead us too far away from basic python.

### Creating a list

The list is a very versatile datatype which can be written as a list of comma-separated values (items) between square brackets. Important  about a list is that items in a list does not need to be of the same type.

Let us take a look at an example:

```python
names = ['Mark', 'Danny', 'Elly', 'Joany', 'Donny']
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9]
characters = ['a', 'b', 'c']
```

Python can print whole list by just supplying them to the print function:

```python
names = ['Mark', 'Danny', 'Elly', 'Joany', 'Donny']
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9]

print(names)
print(numbers)
```

Which would output the following to the console:

```text
['Mark', 'Danny', 'Elly', 'Joany', 'Donny']
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### Accessing elements in a list

Accessing single elements in a list can be achieved by specifying the index of the element between square brackets as shown below.

```python
names = ['Mark', 'Danny', 'Elly', 'Joany', 'Donny']

# Prints "Mark"
print(names[0])
```

You can print them using a for-loop and an iterator `i` created by the range function:

```python
names = ['Mark', 'Danny', 'Elly', 'Joany', 'Donny']

for i in range(0,len(names)):
  print("[{}] {}".format(i, names[i]))
```

Notice the different way of creating a string with values of variables substituted inside the string itself. By adding curly braces where a value is expected and calling the format method on that string, the actual values can be substituted for the curly braces.

The code above would generate the following output:

```text
[0] Mark
[1] Danny
[2] Elly
[3] Joany
[4] Donny
```

When iterating over lists, a for-loop is often written as follows, where the iterator is actually the element of the list itself:

```python
names = ['Mark', 'Danny', 'Elly', 'Joany', 'Donny']

for name in names:
  print(name)
```

The above syntax is much cleaner and more human readable.

Resulting in:

```text
Mark
Danny
Elly
Joany
Donny
```

### Assigning and adding elements to a List

Values in a list can be retrieved using an index, but they can also be assigned a new value in a similar way. Take a look at the example below where a for-loop construct replaces all the elements in the list with their square number.

```python
numbers = [1, 3, 8, 19, 22, 85]

print("Before: " + str(numbers))

for i in range(0, len(numbers)):
  numbers[i] = numbers[i] * numbers[i]

print("After: " + str(numbers))
```

The above cannot be rewritten using a list iterator as this acts as a local variable. The value change would not be reflected to the actual list.

Adding an item to a list can be achieved by using the method `append()` on the list and supplying the method with the item to add.

```python
chars = []

for i in range(0,len("Hello")):
  chars.append("Hello"[i])

print(chars)
```

Notice how a literal string can also be indexing as it were a list.

The previous code results in the output:

```text
['H', 'e', 'l', 'l', 'o']
```
