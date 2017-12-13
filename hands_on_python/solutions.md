## Hands on Python Solutions

### Exercise 1

### Exercise 2

### An LED class

```python
class Led(object):
  def __init__(self):
    self.set_state(False)

  def set_state(self, state):
    self.isOn = state

  def get_state(self):
    return self.isOn
```

or with an even more user-friendly interface:

```python
class Led(object):
  def __init__(self):
    self.off()

  def on(self):
    self.set_state(True)

  def off(self):
    self.set_state(False)

  def set_state(self, state):
    self.isOn = state

  def get_state(self):
    return self.isOn
```

And a little program to test our LED class:

```python
led = Led()
print("LED is " + str(led.get_state()))
led.on()
print("LED is " + str(led.get_state()))
led.off()
print("LED is " + str(led.get_state()))
```
