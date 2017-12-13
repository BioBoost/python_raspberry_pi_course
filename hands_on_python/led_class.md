## An LED class

A light-emitting diode (LED) is a two-lead semiconductor light source. It is a p–n junction diode that emits light when activated. When a suitable voltage is applied to the leads, electrons are able to recombine with electron holes within the device, releasing energy in the form of photons. This effect is called electroluminescence, and the color of the light (corresponding to the energy of the photon) is determined by the energy band gap of the semiconductor. LEDs are typically small (less than 1 mm2) and integrated optical components may be used to shape the radiation pattern.

![A Light Emitting Diode[^1]](img/RBG-LED.jpg)

[^1]: Source https://en.wikipedia.org/wiki/Light-emitting_diode

These days LEDs exist in almost all colors and shapes.

### Modeling an LED in Python

Let us model an LED class that holds the state of an LED.

The state of the LED is saved as an attribute of the object created of the LED class. By adding a getter and setter method we should be able to change the state of the LED.

![Basic LED class](img/basic_led_class.png)

By adding both the state and methods inside a class, we encapsulate all things concerning a LED into a single class.

A class also allows us to reuse the code by enabling us to create multiple LED objects.

### Guide

Start by creating a new python script called for example `led_class.py`.

1. Create a class LED and add a method `set_state` to it that takes in a state as an argument. Assign the value of the argument to an attribute of the class called `state`.

Below is an example of class `Player` that tracks a `nickname` attribute and has a setter method `set_nickname()` for it. Use it as an example to create your setter method for the LED class.

```python
class Player(object):
  def set_nickname(self, nickname):
    self.nickname = nickname
```

2. Next add a constructor method to it called `__init__`. Set the state of the LED to `False` by calling the `set_state` method.

Below is an example of the class `Player` with a constructor that makes use of the `set_nickname` method to set a default nickname. Use it as an example to create your constructor method for the LED class.

```python
class Player(object):
  # ...
  def __init__(self):
    self.set_nickname("Guest")
```

3. Add a getter method `get_state` so the value of that state can be accessed from the outside. Return the value of the `state` attribute.

Below is an example of the class `Player` with a getter method that returns the value of the `username` attribute. Use it as an example to create your getter method for the LED class.

```python
class Player(object):
  # ...
  def get_nickname(self):
    return self.nickname
```

4. Create an object of the LED class at the bottom of your script.

Creating objects of a class can be achieved by stating the name of the class followed by parentheses. To save your new object, you need to assign it to a variable as shown below for a `Player`.

```python
localPlayer = Player()
```

5. Print the state of the LED once the object is created.

Printing the nickname of the `Player` can be done by calling the getter method for the nickname and passing it to the print function:

```python
localPlayer = Player()

print("Nickname of the player is " + localPlayer.get_nickname())
```

6. Change the state of the led by calling the `set_state` method and print out the new state.

This is equivalent to changing the nickname of a Player:

```python
localPlayer = Player()
print("Nickname of the player is " + localPlayer.get_nickname())
localPlayer.set_nickname("Humangus the Fungas")
print("Nickname of the player is " + localPlayer.get_nickname())
```

### Challenge - A More User-friendly Interface to the LED class

Add a method `on()` and `off()` to the class. Call the `set_state` method with the correct state `True` or `False`.

![More User-friendly LED class](img/more_userfriendy_class.png)

Call the methods from your main program to test them. The solution to this can be found at the end of this chapter: [Solutions](../hands_on_python/solutions.md)
