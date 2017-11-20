
# Flow Control Statements

The statements inside your source files are generally executed from top to bottom, in the order that they appear. Control flow statements, however, break up the flow of execution by employing decision making, looping, and branching, enabling your program to conditionally execute particular blocks of code. This section describes the decision-making statements (if-then, if-then-else, switch), the looping statements (for, while, do-while), and the branching statements (break, continue, return) supported by the Python programming language.

## Making Decisions

To allow our program to make certain decisions we first need to take a look at conditions and how they are evaluated.

A condition is some sort of comparison (or a combination of comparisons) that can be evaluated by the compiler or interpreter. After solving all comparisons and combining all the individual parts, the interpreter resolves it to a single resulting value that is `True` or `False` (also keywords in Python). Generally spoken we state that the interpreter evaluates the condition to be true or false.

The true and false values can differ from language to language, however internal in memory false is most of the time "0" and true is "not 0".

### Comparison Operators

The table below shows the available comparison operators that can be used in Python to build a condition.

| Operator | Short Name| Description |
|---|---|
| `==` | equal | If the values of the two operands are equal, then the condition evaluates to `True` |
| `!=` | not equal | If values of the two operands are not equal, then the condition evaluates to `True` |
| `>` | greater than | 	If the value of the left operand is greater than the value of the right operand, then the condition evaluates to `True`. |
| `>=` | greater than or equal to | If the value of the left operand is greater than or equal to the value of the right operand, then the condition evaluates to `True`.
| `<` | less than | If the value of the left operand is less than the value of the right operand, then the condition evaluates to `True`. |
| `<=` | less than or equal to | If the value of the left operand is less than or equal to the value of the right operand, then the condition evaluates to `True`. |

> #### Warning::Deprecated `<>` comparison operator
>
> Some scripts may also use the not-equal operator `<>` which has the exact same meaning as the `!=` operator. However this former is deprecated and even removed in Python 3.x

Since a conditional statement actually produces a single `True` or `Fasle` result, this result can actually be assigned to a variable.

Let's take a look at some examples of comparison operators:

```java
a = 4;
b = 8;
result;
result = (a < b);   // True
result = (a > b);   // False
result = (a <= 4);  // a smaller or equal to 4 - True
result = (b >= 9);  // b bigger or equal to 9 - False
result = (a == b);  // a equal to b - False
result = (a != b);  // a is not equal to b - True
```

Note how we need to use two equality signs `==` to test if two values are equal, while we use a single sign `=` for assignment.

While the comparison operators will not often be used in a situation as shown in the code above, they will often be used when making decisions in your program.
