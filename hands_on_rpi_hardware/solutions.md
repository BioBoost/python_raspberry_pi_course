## Hands on Raspberry Hardware

### Controlling an LED via GPIO

A basic working version could be:

```python
import wiringpi
from time import sleep

class Led(object):
  def __init__(self):
    self.pinNumber = 23
    wiringpi.wiringPiSetupGpio()    # Use GPIO numbering
    wiringpi.pinMode(self.pinNumber, 1)        # Set LED pin to 1 ( OUTPUT )
    self.off()

  def on(self):
    self.set_state(True)

  def off(self):
    self.set_state(False)

  def set_state(self, state):
    self.isOn = state
    wiringpi.digitalWrite(self.pinNumber, state)   # Write 0 ( LOW ) to LED pin

  def get_state(self):
    return self.isOn

led = Led()

for i in range(0,10):
  print("Setting LED on")
  led.on()
  sleep(1)
  print("Setting LED off")
  led.off()
  sleep(1)

print("Done")
```

### Exercise 2

### Exercise 3
