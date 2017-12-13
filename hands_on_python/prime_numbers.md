## Prime Numbers

Getting python in our fingers is best accomplished by doing some work.

A computer is great at quickly carrying out a lot of repetitive work. An example where a computer is so much more effective than a human being is calculating primes. The definition of a prime number is: *a number that is divisible only by itself and 1 (e.g. 2, 3, 5, 7, 11)* Determining how much divisors a random number has can take a lot of time. Python to the rescue!

In this guide we will create a small script that asks the user for a random number and then checks if it is a prime number. To check if it is a prime number we are going to use a loop and the modulo operator.

### Guide

Let us start by asking the user for a number and saving that number in a variable which we than can use further in our script. Remember that we can use the `input()` function to read input from the user.

```python
print("Welcome to our Python Prime Checker app")
numberToCheck = int(input("Please enter a positive number to check for prime: "))
```

Next we need to add a loop construct which tries every number between `2` and `numberToCheck - 1` as a divisors of `numberToCheck`. If any of these divisors result in a modulo (remainder on division) of `0`, then the number is no prime.

A while loop is ideal for this. Let us first implement a while loop that runs for the correct range of divisors and calculates the remainer for each loop.

```python
print("Welcome to our Python Prime Checker app")
numberToCheck = int(input("Please enter a positive number to check for prime: "))

divisor = 2

while divisor < numberToCheck:
  remainder = numberToCheck % divisor
  print(str(numberToCheck) + " % " + str(divisor) + " = " + str(remainder))
  divisor += 1

print("Done")
```

While this is already nice, we do not know yet if the number is a prime number.  An easy option is to check inside the while loop if the remainder is zero, and if it is, increment a counter. If at the end of the while loop the counter is different from `0`, then the given number is not a prime. Also best to remove the print statement inside the while loop.

```python
print("Welcome to our Python Prime Checker app")
numberToCheck = int(input("Please enter a positive number to check for prime: "))

divisor = 2
numberOfDivisors = 0

while divisor < numberToCheck:
  remainder = numberToCheck % divisor
  if remainder == 0:
    numberOfDivisors += 1

  divisor += 1

if numberOfDivisors == 0:
  print(str(numberToCheck) + " is a prime")
else:
  print(str(numberToCheck) + " is NOT a prime")
```

There is one number that is incorrectly threated as a prime and that is the number 1. We need to fix the last if statement to account for this.

```python
print("Welcome to our Python Prime Checker app")
numberToCheck = int(input("Please enter a positive number to check for prime: "))

divisor = 2
numberOfDivisors = 0

while divisor < numberToCheck:
  remainder = numberToCheck % divisor
  if remainder == 0:
    numberOfDivisors += 1

  divisor += 1

if numberToCheck > 1 and numberOfDivisors == 0:
  print(str(numberToCheck) + " is a prime")
else:
  print(str(numberToCheck) + " is NOT a prime")
```

While this code works is it at its best. It would be more reusable and practical if the part that checks the number for being a prime was placed inside a function that can be reused. This can be achieved using the `def` keyword. The function needs to take the number to check as an argument and should return `True` or `False`. This is best practice.

To accomplish this we can create a function called `is_prime` and take the `numberToCheck` as an argument. The code that checks for the prime can be moved from the main program structure and be directly placed in the function. Instead of print statements at the end we can just return `True` or `False`.

```python
def is_prime(numberToCheck):
  divisor = 2
  numberOfDivisors = 0

  while divisor < numberToCheck:
    remainder = numberToCheck % divisor
    if remainder == 0:
      numberOfDivisors += 1

    divisor += 1

  if numberToCheck > 1 and numberOfDivisors == 0:
    return True
  else:
    return False

# The origin part
print("Welcome to our Python Prime Checker app")
numberToCheck = int(input("Please enter a positive number to check for prime: "))

if is_prime(numberToCheck):
  print(str(numberToCheck) + " is a prime")
else:
  print(str(numberToCheck) + " is NOT a prime")
```

The main program code does have to be refactored a bit as shown above. We need to make a call to the function and check the result inside an if-construct. This allows us to print a message to the user.

While the code above works like a charm it can be made a bit shorter and actually also more performant. Simply by returning `False` from inside the while loop once a divisor has been found, indicating that the number is not a prime. This shortens the execution time of the method for primes. At the end of the while we then return `True` as shown below.

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

if is_prime(numberToCheck):
  print(str(numberToCheck) + " is a prime")
else:
  print(str(numberToCheck) + " is NOT a prime")
```

The conditional code

```python
if numberToCheck > 1 and numberOfDivisors == 0:
  return True
else:
  return False
```

can be replaced by the return statement as this code will only be reached if the number is a prime (in the other case the return statement in the while loop made the function return to the calling point.)

### Challenge - Calculating primes

Can you alter the program to show all the primes between 2 and the number the user supplied.

The solution to this can be found at the end of this chapter: [Solutions](../hands_on_python/solutions.md)
