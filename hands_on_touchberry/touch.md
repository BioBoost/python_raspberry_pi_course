## The TouchBerry Pi Touch

The Touchberry Pi shield has been equipped with a capacitive touch sensor (AT42QT1070) and some PCB pads attached to it.

![Front of the Touchberry PI shield](img/front.png)

### The Touchberry Pi shield class

The communication between the capacitive touch sensor and the Raspberry Pi is realized via i2c. A driver for this is supplied by us and accessible via the `TouchberryPi` class.

A UML diagram of the `TouchberryPi` class is shown below.

![UML class diagram of TouchberryPi](img/touchberry_pi_uml.png)

Before you can use the touch interface you will need to import some classes into your application.

```python
from touchberrypi import TouchberryPi
from touchberrypi import TouchKey
```

To make use of the shield driver you will need to make an object of the `TouchberryPi` class.

```python
shield = TouchberryPi()
```

![UML diagram of TouchKey and KeyState enums](img/touchberry_pi_touch_uml.png)

### Getting Notified of Touch Events

When someone touches one of the pads of the Touchberry Shield an event is generated. At the moment this event is ignored by our library. However you as a user of the `TouchberryPi` class can ask the shield to get notified of these events by registering a method that needs to be called when the event happen. We speak of registering a callback method.

Let us for example register a callback method when a pad is being pressed.

1. Creating a method that needs to be called when a key is pressed:

```python
from touchberrypi import TouchberryPi
from touchberrypi import TouchKey

def on_key_down(key):
    print("Key {} down".format(key))
```

Do note that the key that is pressed needs to be passed as an argument to the event handler.

2. Next we need to create a `TouchberryPi` object and register our method as a key event handler. Do make sure to place the variable above the `on_key_down` method as later on we will need to be able to access it from inside the method.

```python
from time import sleep
from touchberrypi import TouchberryPi
from touchberrypi import TouchKey

shield = TouchberryPi()

def on_key_down(key):
    print("Key {} down".format(key))

shield.on_key_down(on_key_down)
```

3. Last we need tell the shield to start capturing touch events. This is achieved by calling the method `start_touch_listener()` on the shield and passing the check interval in seconds (can be a float - smaller intervals make it more responsive). An endless loop was also added to ensure the script keeps running.

```python
from time import sleep
from touchberrypi import TouchberryPi
from touchberrypi import TouchKey

shield = TouchberryPi()

def on_key_down(key):
  print("Key {} down".format(key))

shield.on_key_down(on_key_down)
shield.start_touch_listener(0.1)

while True:
  sleep(1)
```

4. Now we can check which key was pressed by checking the key argument as shown below. The key needs to be compared against the known enum values of `TouchKey`.

```python
from time import sleep
from touchberrypi import TouchberryPi
from touchberrypi import TouchKey

shield = TouchberryPi()

def on_key_down(key):
  print("Key {} down".format(key))
  if key == TouchKey.UP:
    print("Pressing the up key")
  elif key == TouchKey.DOWN:
    print("Pressing the down key")

shield.on_key_down(on_key_down)
shield.start_touch_listener(0.1)

while True:
  sleep(1)
```

5. The same can now also be done for a key being released.

```python
from time import sleep
from touchberrypi import TouchberryPi
from touchberrypi import TouchKey

shield = TouchberryPi()

def on_key_down(key):
  print("Key {} down".format(key))
  if key == TouchKey.UP:
    print("Pressing the up key")
  elif key == TouchKey.DOWN:
    print("Pressing the down key")

def on_key_up(key):
  print("Key {} up".format(key))
  if key == TouchKey.UP:
    print("Releasing the up key")
  elif key == TouchKey.DOWN:
    print("Releasing the down key")

shield.on_key_down(on_key_down)
shield.on_key_up(on_key_up)
shield.start_touch_listener(0.1)

while True:
  sleep(1)
```

### Challenge

1. Change the code above to create a running light (aka Nightrider light). To do this you need to:
 1. Import the Led libraries (see previous guide)
 2. Create a variable to hold the current LED index (the one that is turned on)
 3. Use the `shield.set_led` method to turn off the current LED and turn on the next. Do this in the while loop
 4. sleep for some time after changing the LEDs

2. Use the UP and DOWN key to increase or decrease the delay interval inside the while loop. Effectively allowing us to slow down or speed up the running light.

3. Use the X key to change the color of the running light. You will need to create a list of colors and keep an indexing variable.

The full solution can be found in the solutions section.
