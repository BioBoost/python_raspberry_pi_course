## Operators

### Mathematical Operators

The Python programming languages has a lot of operators. Two operators have already been discussed, namely the assignment operator `=` and the string concatenation operator `+`.

The most basic operators are the mathematical operators. They are easy to understand because they have the same functionality as in math. The following operators are available to do basic math operations:

* `+` Additive operator (also used for String concatenation)
* `-` Subtraction operator
* `*` Multiplication operator
* `/` Division operator
* `%` Remainder operator
* `**` Power operator
* `//` Floor division operator

These operators are part of the **binary operators** because they take **two operands**, namely a left and a right operator. Both of the operands can be either a literal value (such as `12`) or a variable. For example in the summation below `left` is the left operand and `right` is the right operand. The result of the operation is stored in the variable `total`.

```python
right = 14
left = 12

total = left + right
# total is now 26
```

The `+`, `-` and `*` operators function the same as in math. Their use can be seen in the code below.

```python
a = 2 + 3
print("a = " + str(a))
# a = 5

b = a + 5
print("b = " + str(b))
# a = 10

c = 6 * b
print("c = " + str(c))
# c = 60

d = c - 120;    // d = -60
print("d = " + str(d))
# d = -60

print("Two to the fourth power:")
print(2**4)
# 16
```

The power operator `**` takes as a left operand the base number and as a right number the power.

The division and remainder operators deserve some special attention. The division operator has a different result based on the types of its left and right operand. If both are of an integral type then a whole division will be performed. Meaning that `3 / 2` will result in `1`. If either operand is a floating point operand than the division operator will perform a real division: `3.0 / 2` will result in `1.5`. The remainder operator will give you the remainder after a whole division.

If your operands are of integral type and you wish to perform a real division, you can always multiply one of the operands with `1.0` to explicitly convert it to a floating point number. Or you can use a `float()` cast.

The floor division operator `//` will always perform a real division but will floor the result.

Let us take a look at some examples.

```python
x = 5
y = 2

z = x / y
print("z = " + str(z))    #  (whole division)
# z = 2

# Attention this is still a whole division
# but the result is converted to float
w = float(x / y)
print("w = " + str(w))
# w = 2.0

q = float(x) / y          # (real division)
print("q = " + str(q))
# q = 2.5

t = 1.0 * x / y          # (real division)
print("t = " + str(t))
# t = 2.5

r = x % y                # Remainder
print("r = " + str(r))
# r = 1
```

Notice that even `w = float(x / y)` results in `2.0`. The reason behind this is that `x / y` equals to `2` as it is a whole division since both operand are of integral type. The result is then cast to a float, and stored in `w`.

While the precedence (order) in which mathematical operations are performed is defined in Python, most programmers do not know all of them by heart. It is much more clear and simpler to use round brackets `()` to enforce the precedence of the calculations.

### Compound Operators

Programmers are very lazy creatures that are always looking for ways to make their life's easier. That is why the compound operators were invented. They are a way to write shorter mathematical operations on the same variable as the result should be store in.

```python
x = 5;

x += 4    # Same as writing x = x + 4
x -= 4    # Same as writing x = x - 4
x *= 4    # Same as writing x = x * 4
x /= 4    # Same as writing x = x / 4
x %= 4    # Same as writing x = x % 4
x //= 4   # Same as writing x = x // 4
x **= 4   # Same as writing x = x ** 4
```
