## Hands on Python Solutions

### Prime Numbers

The script below determines all the prime numbers up until a user specified number.

```python
def is_prime(numberToCheck):
  divisor = 2

  while divisor < numberToCheck:
    remainder = numberToCheck % divisor
    if remainder == 0:
      return False

    divisor += 1

  return True

# The original part
print("Welcome to our Python Prime Checker app")
numberToCheck = int(input("Please enter a positive number to check for prime: "))

print("Primes: ")
for number in range(1,numberToCheck):
    if is_prime(number):
        print(str(number), end=' ')
```

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
